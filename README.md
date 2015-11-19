# Ansible role `Siege`
Installs the loadtesting tool siege 3.1.0 on centos7 as a role in an ansible environment.

An Ansible role for installing `Siege` on RHEL/CentOS 7. Specifically, the responsibilities of this role are to:

- Install Siege version 3.1.0
- Set up the host as a server

## What is Siege?
Siege is a benchmarking and load testing tool that can be used to measure the performance of a web server when under immense pressure. Siege performs following tests:
- Amount of data transferred.
- Response time of server.
- Transaction rate.
- Throughput.
- Concurrency.
- Times the program returned ok.

## Siege provides three modes of operation:

Regression.
Internet Simulation.
Brute Force.

For more information about this loadtesting tools, I recommend to visit the [`Official website`](https://www.joedog.org/siege-home/).

The following things will be done during the installation of this role:
- Update and upgrade your server
- Install Siege version 3.1.0
- install the `Development tools` package group

## Getting started


## Requirements

At this moment, we are using a vagrant-environment. The role will be installed in the home directory of the vagrant-host. More info about how to use Vagrant, u can find [`here`] (https://docs.vagrantup.com/v2/).

## Important files
### .siegerc
As mentioned before, the roll will be installed in the home directory of the vagrant host ( `Home/vagrant/` ). If you use the `list -a` -command in this directory, you will notice a file called `.siegerc` .

In this file you got the opportunity to edit the settings of your load. For example you can change howmany concurrent users will be simulated. By default Siege configuration suggests 25 concurrent users over a period of 1 minute. 
List of settings you can edit here.

| Variabele 	| Default 	| Example 	| Comments 	|
|---------------------------	|-----------------------------------------	|---------------------------------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| `PROXY ` 	| - 	| `PROXY = proxy.joedog.org` 	| You can set variables here for use in the directives below 	|
| `proxy-host` 	| - 	| `proxy-host = ${PROXY}` 	| Reference variables inside `${}` or `$()` 	|
| `logfile` 	| `/usr/local/var/siege.log` 	| `logfile = $(HOME)/var/siege.log` 	| You can also reference ENVIRONMENT variables without actually declaring them. Note: The default log-file will be created after the first time you run siege. 	|
| `verbose` 	| `true` 	| `verbose = true|false` 	| Signify verbose mode, `true` turns on verbose output. 	|
| `quiet mode` 	| `false` 	| `quiet = false` 	| When `true`, this turns off verbose and standard output. You'll still see the opening announcement  and the final stats if you're running a siege but `-g/--get` will be extremely quiet.  This was added primarily for scripting. 	|
| `gmethod` 	| `HEAD` 	| `gmethod = GET` 	| Get method - select an HTTP method to use when siege is set to get mode, `siege -g/--get` URL. You may select GET or HEAD. HEAD prints just the headers and GET prints the entire page. 	|
| `CSV` 	| `false` 	| `csv = true|false` 	| With this option, you can choose to format verbose output in traditional siege format  or comma separated format 	|
| `Timestamp` 	| `false` 	| `timestamp = true|false` 	| With this option, you can choose to print a timestamp each line of output. 	|
| `fullurl` 	| `false` 	| `fullurl = true|false` 	| By default siege displays the URL path and not the full URL. With this option,  you can instruct siege to show the complete URL. 	|
| `display-id` 	| `false` 	| `display-id = true|false` 	| Display the siege user id associated with the HTTP transaction information. 	|
| `show-logfile` 	| 'true' 	| `show-logfile = true|false` 	| By default, siege displays the logfile location at the end of every run when logging. You can turn this message off with this directive. 	|
| `logging` 	| `true` 	| `logging = true|false` 	| Default logging status, `true` turns logging on 	|
| `log-file` 	| `usr/local/var/siege.log` 	| `logfile = ${HOME}/var/log/siege.log` 	| This directive allows you to choose an alternative log file. 	|
| `protocol` 	| `HTTP/1.1` 	| `protocol = HTTP1.0` 	| Some webservers have broken implementation of the 1.1 protocol  which skews throughput evaluations.If you notice some siege clients hanging for extended periods of time, change this to HTTP/1.0 	|
| `chunked` 	| `true` 	| `chunked = true|false` 	| Chunked encoding is required by HTTP/1.1 protocol but siege allows you to turn it off as desired. 	|
| `cache` 	| `false` 	| `cache = true|false` 	| Siege supports cache revalidation for both ETag and Last-modified headers.  If a copy is still fresh, the server responds with 304. 	|
| `connection` 	| `close` 	| 'connection = keep-alive' 	| Siege implements persistent connections in accordance to RFC 2068 using both chunked encoding and content-length directives to determine the page size. To run siege with persistent connections set the connection directive to keep-alive. 	|
| `concurrent` 	| `15` 	| `concurrent = 25` 	| Default number of simulated,concurrent users 	|
| `time` 	| `1M` 	| `time = 5S` 	| Default duration of the siege.,The right hand argument has a modifier which specifies the time units, H=hours, M=minutes, and S=seconds. 	|
| `reps` 	| - 	| `reps = 20` 	| The length of siege may be specified in client reps rather then a time duration. Instead of specifying a time span, you can tell each siege instance to hit the server X number of times. So if you chose 'reps = 20' and you've selected 10 concurrent users, then siege will hit the server 200 times. 	|
| `file` 	| - 	| `file = $HOME/etc/urls.txt` 	| Use the "file = " directive to configure an alternative URLs file.  You may use environment variables 	|
| `url` 	| - 	| `url = https://shemp.whoohoo.com/docs/index.jsp` 	| This is a single URL that you want to test. This is usually set at the command line with the `-u` option.When used, this option overrides the urls.txt 	|
| `delay` 	| `1` 	| `delay = 5` 	| This value is used for load testing, it is not used for benchmarking. In secondes. 	|
| `timeout` 	| `30` 	| `timeout=30` 	| Connection timeout value. Set the value in seconds for socket connection timeouts. 	|
| ´expire-session` 	| `false` 	| `expire-session = true|false` 	| This directive allows you to delete all cookies after you pass through the URLs. This means siege will grab a new session with each run through its URLs. 	|
| `cookies` 	| `true` 	| `cookies = true|false` 	| This directive is available to disable that support. Set cookies to `false` to refuse cookies. 	|
| `failures` 	| `1024` 	| `failures = 50` 	| This is the number of total connection failures allowed before siege aborts. 	|
| `internet` 	| `false` 	| `internet = true|false` 	| Internet simulation. If `true`, siege clients will hit the URLs in the urls.txt file randomly, thereby simulating internet usage,If `false`, siege will run through the urls.txt file in order from first to last and back again. 	|
| `benchmark` 	| `false` 	| ´benchmark = true|false` 	| Default benchmarking value, If `true`, there is NO delay between server requests, siege runs as fast as the web server and the network will let it.,Set this to `false`  for load testing. 	|
| `user-agent` 	| `JoeDog/1.00 [en] (X11; I; Siege #.##)` 	| `user-agent = Limey The Bulldog` 	| Set the siege User-Agent to identify yourself at the host 	|
| `accept-encoding` 	| `gzip` 	| `accept-encoding = compress;q=0.5;gzip;q=1` 	| This option allows you to specify acceptable encodings returned by the server.  Use this directive to turn on compression 	|
| `url-escaping` 	| `true` 	| `url-escaping = true|false` 	| URL escaping was added in version 3.0.3. You may use this directive to turn off this experimental feature. By default this feature is active by default starting with v3.0.3 	|
| `spinner` 	| `true` 	| `spinner = true|false` 	| Siege spawns a thread and runs a spinner to entertain you as it collects and computes its stats. If you don't like this feature, you may turn it off here. 	|
| `login` 	| `all` 	| `login = jdfulmer:topsecret:Admin` 	| WWW-Authenticate login.When siege hits a webpage that requires basic authentication, it will search its logins for authentication which matches the specific realm requested by the server. The format for logins is username:password[:realm] where "realm" is optional. 	|
| `login-url` 	| - 	| `login-url = http://www.haha.com/login.php?name=homer&pass=whoohoo` 	| This is the first URL to be hit by every siege client. This feature was designed to allow you to login to a server and establish a session. 	|
| `FTP login` 	| - 	| `ftp-login: jdfulmer:password` 	| FTP login.This directive provides one of two ways # to login to an ftp server. The format is USER:PASS:HOST separated by colon ':' The host field is optional. 	|
| `unique` 	| `true` 	| `unique = true|false` 	| This directive determines whether siege will upload files with the same name (and therefore overwrite whatever is on disk) or upload files each with a unique name. 	|
| `SSL-cert` 	| - 	| `ssl-cert = /home/jeff/.certs/cert.pem` 	| This optional feature allows you to specify a path to a client certificate. 	|
| `ssl-key` 	| - 	| `ssl-key home/jeff/.certs/client.pem` 	| Use this option to specify the key you generated with the command above. 	|
| `ssl-timeout` 	| - 	| `ssl-timeout=30` 	| This option sets a connection timeout for the ssl library. In secondes. 	|
| `ssl-ciphers` 	| - 	| `ssl-ciphers = EXP-RC4-MD5` 	| You can use this feature to select a specific ssl cipher for HTTPs. To view the ones available with your library run the following command: `openssl ciphers` 	|
| `proxy-host` `proxy-port` 	| - 	| `proxy-host = proxy.joedog.org` `proxy-port = 3123` 	| You can use siege to test a proxy server but you need to configure it to use one. You'll need to name a proxy host and the port it's listening one. 	|
| `proxy-login ` 	| - 	| `proxy-login: jeff:secret:corporate` 	| Proxy-Authenticate. When scout hits a proxy server which requires username and password authentication, it will this username and password to the server. 	|
| `follow-location` 	| - 	| `follow-location = true|false` 	| This option allows to to controlwhether a Location: hint will be followed. Most users will want to follow redirection information, but sometimes  it's desired to just get the Location information. 	|
| `zero-data-ok` 	| - 	| `zero-data-ok = true|false` 	| Zero-length data. Siege can be configured to disregard results in which zero bytes are read after the headers. Alternatively, such results can be counted in the final tally of outcomes. 	|
### Log-file





## Contributing

Mathias Van Rumst


## License

BSD

## Author Information

Jens De Vreese
