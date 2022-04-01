# Axios calls review


Axios is a fantastic library that we can use to run CRUD Functionality in our apps.
We will need to create the necessary routes on our back end to match our AXIOS Async API calls

Any information that is in ALL CAPS, "data", or surrounded by <>'s is something that you'll need to fill in with your own respective information based on your project.


### Back End :
First, lets set up our Controllers for our data


```js

//Controllers.js

const Data = require('../models/data');

const getAllData = async (req, res) => {
  try {
    const tips = await Data.find();
    return res.status(200).json({ data });
  } catch (error) {
    return res.status(500).send(error.message);
  }
};

const getDataById = async (req, res) => {
  try {
    const { id } = req.params;
    const data = await Data.findById(id);
    if (data) {
      return res.status(200).json({ data });
    }
    return res.status(404).send('Data with the specified ID does not exist');
  } catch (error) {
    return res.status(500).send(error.message);
  }
};


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
Then we can set up our routes, linked to our controllers


```js
//Routes

const { Router } = require('express');
const router = Router();
const controllers = require('../controllers');

router.get('/api', (req, res) => res.send('This is root!'));

router.get('/data', controllers.getAllData);
router.get('/data/:id', controllers.getdataById);
router.post('/addData', controllers.createData);
router.put('/updateData/:id', controllers.updateData);
router.delete('/data/:id', controllers.deleteData);


```

### Front End Axios Commands :

```js


//Create 
   //our initial state for our Create Form
     const [form, setForm] = useState({
       name: '',
       description: ''
     });


    //stately forms
    const handleForm = async (e) => {
      await setForm({ ...form, [e.target.name]: e.target.value });
      console.log(form);
  };

    //Axios call, linked to our stately form
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
// if '.id' is not working, try '._id'

  const handleDelete = async (e) => {
    e.preventDefault();
    await axios.delete(`${BASE_URL}/<COLLECTION>/${e.target.id}`);
    window.location.reload();
  };


```

