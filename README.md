# Axios calls review


Axios is a fantastic library that we can use to run CRUD Functionality in our apps.
We will need to create the necessary routes on our back end to match our AXIOS Async API calls

Any information that is in ALL CAPS and surrounded by <>'s is something that you'll need to fill in with your own respective information based on your project.


Back End Routes :
```js

//Controllers.js

const createData = async (req, res) => {
  try {
    const data = await new Data(req.body);
    await data.save();
    return res.status(201).json({
      data
    });
  } catch (error) {
    return res.status(500).json({ error: error.message });
  }
};

const updateData = async (req, res) => {
  try {
    const { id } = req.params;
    await Data.findByIdAndUpdate(id, req.body, { new: true }, (err, data) => {
      return res.status(200).json(data);
    });
  } catch (error) {}
};

const deleteData = async (req, res) => {
  try {
    const { id } = req.params;
    const deleted = await Data.findByIdAndDelete(id);
    if (deleted) {
      return res.status(200).send('Data deleted');
    }
    throw new Error('Data not found');
  } catch (error) {
    return res.status(500).send(error.message);
  }
};


```

Front End Axios Commands :

```js


//Create 
   //our initial state for our Create Form
     const [form, setForm] = useState({
       name: '',
       description: ''
     });


    //stately form code
  
    const handleForm = async (e) => {
      await setForm({ ...form, [e.target.name]: e.target.value });
      console.log(form);
  };


    //actual call
    const handleCreate = async (e) => {
      e.preventDefault();
      await axios.post(`${BASE_URL}/add<DATA>`, form);
  };
    
     




//Read

   const getData = async () => {
    const res = await axios.get(`${BASE_URL}/<COLLECTION>`);
    setTips(res.data.<DATA_NAME>)/;
  };



//Delete

  const handleDelete = async (e) => {
    e.preventDefault();
    await axios.delete(`${BASE_URL}/<COLLECTION>/${e.target.id}`);
    window.location.reload();
  };


```

