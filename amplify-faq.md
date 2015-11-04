## 1. General

### 1.1. What is NGINX Amplify

NGINX Amplify is a monitoring and configuration help product. It is a SaaS product, and it's hosted on AWS public cloud.

In order to be able to use NGINX Amplify to monitor your infrastructure, you need to install Amplify Agent on each system that has to be checked.

You can use NGINX Amplify to do the following:

 * Keep track of the systems running NGINX
 * Proactively identify issues related to NGINX configuration and operations
 * Find bottlenecks in NGINX infrastructure
 * Improve and optimize NGINX configuration and setup
 * Plan web applications capacity and performance
 
`Visualize your web server performance
Correlate the performance of Nginx with the rest of your applications`
 
### 1.2. Where is the main system hosted

NGINX Amplify SaaS is currently hosted in [AWS us-west-1](http://docs.aws.amazon.com/general/latest/gr/rande.html) (US West, N. California).

### 1.3. Is the traffic from the agent to the SaaS protected?

All communications between the Amplify Agent and the Amplify SaaS are done securely over TLS/SSL, using 2048-bit encryption.


## 2. User interface

### 2.1. What browsers are supported

Currently the following desktop browsers are officially fully supported:

 * Chrome
 * Firefox
 * Safari



## 3. Metrics and metadata

### 3.1. What metrics and metadata is collected

The agent collects the following type of data:

 * **System metadata.** This is basic information about the OS environment where the agent runs. This could be hostname, uptime information, and so on.
 * **System metrics.** This is various data describing key system characteristics, e.g. CPU usage, memory usage, network traffic etc.
 * **NGINX metadata.** This is what describes your NGINX instances, and it includes a particular package and build information, path to binary, configure options etc. NGINX metadata also includes config file breakdown.
 * **NGINX metrics.** Amplify Agent collects NGINX related metrics from [stub_status](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html), and also from the NGINX logs files.

### 3.2. How is the NGINX configuration parsed and analyzed

Amplify Agent is able to automatically find all relevant NGINX configuration files, parse configuration, extract their logical structure and send them to Amplify SaaS for further analysis and reports. For more information on configuration analysis and reports see the Amplify documentation.


## 4. Amplify Agent

### 4.1. What operatings systems are supported

Amplify Agent is currently supported on select Linux flavors only — that's Ubuntu, Debian and CentOS.

### 4.2. How to add a new a system to the monitoring?

This is done as simple as:

 1. Download and run install script.

        # curl -sS -L -O http://pp.nginx.com/andrew/files/install.sh && \
        API_KEY='ecfdee2e010899135c258d741a6effc7' sh ./install.sh`
     
    (where API_KEY is a unique API key assigned when you create an account with Amplify)

 2. Start Amplify Agent.

        # /etc/init.d/amplify-agent start

### 4.3. What do I need to get the Agent reporting metrics?

After you install and start the agent, normally it should just start reporting right away, pushing aggregated data to the SaaS in regular 1m intervals. It'll take about a minute for the new system to appear in the Amplify Web UI.

If you don't see the new system in the UI, or metrics aren't being collected, please make sure that:

 1. Amplify Agent package has been successfully installed
 2. `amplify-agent` process is running
 3. [stub_status](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html) is properly set up in your NGINX configuration
 4. NGINX [access.log](http://nginx.org/en/docs/http/ngx_http_log_module.html) and [error.log](http://nginx.org/en/docs/ngx_core_module.html#error_log) files are readable by the user `nginx` (or by the [user](http://nginx.org/en/docs/ngx_core_module.html#user) configured in NGINX config)
 5. oubound TLS/SSL from the system is not restricted
 6. system DNS resolver is properly configured, and `receiver.amplify.nginx.com` can be successfully resolved

### 4.4. How to verify if the Amplify Agent is properly installed

 1. On Ubuntu/Debian

```
    # dpkg -s nginx-amplify-agent
    Package: nginx-amplify-agent
    Status: install ok installed
    Priority: optional
    Section: python
    Maintainer: Mike Belov
    Architecture: amd64
    Version: 0.20-1~trusty
    Depends: python (>= 2.6), lsb-release
    Description: Nginx Amplify Agent
    Homepage: https://www.nginx.com/
```

 2. On CentOS

```
    XXXX
```

### 4.5. How to update the agent?

 1. On Ubuntu/Debian use
 
```
    apt-get update && \
    apt-get install nginx-amplify-agent && \
    service amplify-agent restart
```

 2. On CentOS use

```
    XXXX
```

### 4.6. How much system resources are required?

We tried very hard to make the agent retain as small memory and CPU footprint as possible. Normally it shouldn't be more than a few % of CPU time, and around 25-30MB of RSS memory.
   
### 4.7. How to restart the agent

 1. On Ubuntu/Debian

```
    service amplify-agent restart
```

 2. On CentOS

```
    XXXX
```


