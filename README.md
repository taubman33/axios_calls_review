# Axios calls review


Axios is a fantastic library that we can use to run CRUD Functionality in our apps.
We will need to create the necessary routes on our back end to match our AXIOS Async API calls



Back End Routes :





Front End Axios Commands :

```js

//Delete

  const handleDelete = async (e) => {
    e.preventDefault();
    await axios.delete(`${BASE_URL}/<COLLECTION>/${e.target.id}`);
  };


```

