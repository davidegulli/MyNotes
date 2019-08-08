## Basic auth in ajax request

```javascript
fetch("/api/jsonws/user/get-company-users", {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': 'Basic ' + btoa('test@liferay.com:test')
    },
    body: JSON.stringify({
        companyId: 20099,
        start: 0,
        end: 100
    })
})
.then(res => res.json());	      
```

