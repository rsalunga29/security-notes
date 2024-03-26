We may also be able to identify unused parameters or APIs in the front-end code in the form of JavaScript AJAX calls. Some web applications developed in JavaScript frameworks may insecurely place all function calls on the front-end and use the appropriate ones based on the user role.

For example, the following example shows a basic example of an AJAX call:
```javascript
function changeUserPassword() {
    $.ajax({
        url:"change_password.php",
        type: "post",
        dataType: "json",
        data: {uid: user.uid, password: user.password, is_admin: is_admin},
        success:function(result){
            //
        }
    });
}
```
The above function may never be called when we use the web application as a non-admin user. However, if we locate it in the front-end code, we can modify the parameter values to change another user's password or elevate a user account into admin.