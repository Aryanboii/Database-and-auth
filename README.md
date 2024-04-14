# Database-and-auth

function getAnimalData() {
    fetch("https://fakerapi.it/api/v1/persons")
        .then(function(response) {
            return response.json(); // Return the JSON promise
        })
        .then(function(finalData) {
            console.log(finalData);
        })
        .catch(function(error) {
            console.error("Error fetching data:", error); // Optional error handling
        });
}


/// async fun
 async function getAnimaldata(){
     const response = await fetch("https://fakerapi.it/api/v1/persons");
     
     
    const finaldata =  await response.json()
         console.log(finaldata);
    
}

// Assingment -> A website which h two endpoints

const express = require("express");
const jwt = require("jsonwebtoken"); // libraries implementation of json web tokens
const { allowedNodeEnvironmentFlags } = require("process");
const jwtPassword = "1234556";

app.use(express.json());

const ALL_USERS = [
    {
      username: "aryanarya1206@.com",
      password: "123",
      name: "harkirat singh",
    },
    {
      username: "raman@gmail.com",
      password: "123321",
      name: "Raman singh",
    },
    {
      username: "priya@gmail.com",
      password: "123321",
      name: "Priya kumari",
    },
  ];
  
// write logic to return T or F
  function userExist(username, password){
    let userExist = false;
    for(let i=0; i<ALL_USERS.lengthl; i++){
     if(ALL_USERS[i].username== username&& ALL_USERS[i].password){
      userExist =true;
     }
    }
    return userExist;
  }




app.post("/signin",function(req,res){
    const username = req.body.username;
    const password = req.body.password;

    if(!userExist(username,password)){
      return res.status(403).json({
        msg : "user doesnt exist in our DB",
      });
    }


    var token = jwt.sign({username : username},jwtPassword);
    return res.json({
      token,
    });



});


app.get("/users",function(req,res){
  const token = req.headers.authorization;
  try{
    const decoded =jwt.verify(token,jwtPassword);
    const username = decoded.username;

    // return a list of users other than this username

    res.json({
      users : ALL_USERS.filter(function(value){
        if(value.username ==  username){
          return false
        } 
        else{
          return true;
        }
      })
    })



  } catch(err){
    return req.status(403).json({
      msg : "Invalid token",
    });
  }
});
app.listen(3000) 
