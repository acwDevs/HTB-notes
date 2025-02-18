
##### Modifying request sent to Back-End
**Note:** We need to edit the filename part of the header and file content at end of request

```
filename="HTB.png" -> filename="HTB.php"
```
![[Pasted image 20250210222316.png]]
**Note:** We may also modify the `Content-Type` of the uploaded file


#### Disable Front-End Validation

This can be done by analyzing source code to check if the front end has any validation
If there is front end validation we can either edit the javascript or html to bypass validation
E.g
```html
<input type="file" name="uploadFile" id="uploadFile" onchange="checkFile(this)" accept=".jpg,.jpeg,.png">
```
**Note:**Front-End javascript file check called checkFile(this)


