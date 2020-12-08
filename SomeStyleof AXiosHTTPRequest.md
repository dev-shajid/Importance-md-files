> Javascript Http fetch Request

```
const data = { username: 'example' };

fetch('https://example.com/profile', {
  method: 'POST', // or 'PUT'
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(data),
})
.then(response => response.json())
.then(data => {
  console.log('Success:', data);
})
.catch((error) => {
  console.error('Error:', error);
})
```



> send a POST request

```
axios({
  method: "post",
  url: "/login",
  data: {
    firstName: "Finn",
    lastName: "Williams",
  },
});
```

> Login Request

```
axios.post("/login", {
  firstName: "Finn",
  lastName: "Williams",
});
```

> Asios reqyest

```
axios
  .post("/login", {
    firstName: "Finn",
    lastName: "Williams",
  })
  .then(
    (response) => {
      console.log(response);
    },
    (error) => {
      console.log(error);
    }
  );
```

> axi os

```
axios.get("https://api.github.com/users/mapbox").then((response) => {
  console.log(response.data);
  console.log(response.status);
  console.log(response.statusText);
  console.log(response.headers);
  console.log(response.config);
});
```

> execute simultaneous requests

```
axios
  .all([
    axios.get("https://api.github.com/users/mapbox"),
    axios.get("https://api.github.com/users/phantomjs"),
  ])
  .then((responseArr) => {
    //this will be executed only when all requests are complete
    console.log("Date created: ", responseArr[0].data.created_at);
    console.log("Date created: ", responseArr[1].data.created_at);
  });
```

> Multi line

```
axios
  .all([
    axios.get("https://api.github.com/users/mapbox"),
    axios.get("https://api.github.com/users/phantomjs"),
  ])
  .then(
    axios.spread((user1, user2) => {
      console.log("Date created: ", user1.data.created_at);
      console.log("Date created: ", user2.data.created_at);
    })
  );
```

> send Options

```
const options = {
  headers: { "X-Custom-Header": "value" },
};

axios.post("/save", { a: 10 }, options);
```

> hello

```
const options = {
  method: "post",
  url: "/login",
  data: {
    firstName: "Finn",
    lastName: "Williams",
  },
  transformResponse: [
    (data) => {
      // transform the response

      return data;
    },
  ],
};

// send the request
axios(options);
```
