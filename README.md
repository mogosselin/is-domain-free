# Is Domain Free - Lookup availability of a domain name

It's a simple library that checks if a domain name is available or not. It uses the system's command 'whois' to check for availability. Since it checks the result of the 'whois' and it can be different for different domain names, it's currently limited to .io, .net and .com domains, but it can be easily extended.

# Basic usage

## Single check

```python
from is_domain_free import is_free
if is_free('google.com'):
    print('Google.com is free!')
else:
    print('Google.com is taken!')
```

## Multiple checks

If you need to check a batch of domain names, use this method (and not is_free in a loop) since the batch check uses multiple processes in parallel and is faster.

```python
from is_domain_free import are_free

domains = ['google.com', 'rewqqwerty.com', ...]
result = are_free(domains)

# result will be [('google.com', False), ('rewqqwerty.com', True), ...]
```

# WHOIS command

For the program to work, it needs a 'whois' command, which is not available by default on Windows, but can be downloaded here: https://docs.microsoft.com/en-ca/sysinternals/downloads/whois

# Extending 

There are 2 main classes that are targets for extensions:

1. WhoisGetter: This class will read the content of a whois command and return the result (string). This class simply needs a method called `get_whois_content(domain)` which would return the content of a whois as a text string. You could extend it (or just create a new class with the method) if you want to use something else then calling 'whois xyz.com' from the command line.
2. WhoisParser: This class reads the content of a 'whois' and decides if the domain name specified is available or not based on that content. You can extend it if you whish to support more domain names, for example, or change how the parser decides if a domain name is taken or not.

# DomainNameAvailabilityChecker

That's the main class that 'assembles' both WhoisGetter and WhoisParser, so it shouldn't be necessary to change it / extend it.

