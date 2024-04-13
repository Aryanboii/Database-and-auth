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
