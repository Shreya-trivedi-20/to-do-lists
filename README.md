# to-do-lists
<!doctype html>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
        integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

    <title>TODOs List</title>
</head>

<body>
    <style>
        body{
            background-color: gold;
            border:midnightblue;
        }
        #titlecolor{
            color:maroon
        }
        #descolor{
            color:maroon
        }
        #a{
            color:mediumblue;
        }
        #b{
            color:mediumblue;
        }
        #c{
            color:mediumblue;
        }
        #d{
            color:mediumblue;
        }
        .table{
            border:olivedrab;
        }
    </style>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand" href="#">TODOs List</a>
    </nav>

    <div class="container my-4">
        <h2 class="text-center">TODOs List</h2>
         
            <div class="form-group">
                <label for="title" id ="titlecolor"><strong>Title</strong></label>
                <input type="text" class="form-control" id="title" aria-describedby="emailHelp">
                <small id="smalltext" class="form-text text-muted">Add your task</small>
            </div>

            <div class="form-group">
                <label for="description" id="descolor"><strong>Description</strong></label>
                <textarea class="form-control" id="description" rows="3"></textarea>
            </div>
            

            <button   id="add" class="btn btn-success">Add to list</button>
            <button  id="clear" class="btn btn-danger" onclick="clearStorage()">Clear list</button>
         

        <div id="items" class="my-4">
            <h2>Task i will perform</h2>
            <table class="table">
                <thead>
                  <tr>
                    <th scope="col" id ="a"><strong>Sno:</strong></th>
                    <th scope="col" id="b"><strong>Title of task</strong></th>
                    <th scope="col" id="c"> <strong>Details of  the task</strong></th> 
                    <th scope="col" id ="d"><strong>delete this task</strong></th> 
                  </tr>
                </thead>
                <tbody id="tableBody">
                  <tr>
                    <th scope="row">1</th>
                    <td>My task</td>
                    <td>description of my task</td> 
                    <td><button class="btn btn-sm btn-dark">Delete</button></td> 
                  </tr>
                  
                </tbody>
              </table>
        </div>
    </div>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
        integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
        crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"
        integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo"
        crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"
        integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI"
        crossorigin="anonymous"></script>
        <script>
            function getAndUpdate(){
                console.log("Updating List...");
                tit = document.getElementById('title').value;
                desc = document.getElementById('description').value;
                if (localStorage.getItem('itemsJson')==null){
                    itemJsonArray = [];
                    itemJsonArray.push([tit, desc]);
                    localStorage.setItem('itemsJson', JSON.stringify(itemJsonArray))
                }
                else{
                    itemJsonArrayStr = localStorage.getItem('itemsJson')
                    itemJsonArray = JSON.parse(itemJsonArrayStr);
                    itemJsonArray.push([tit, desc]);
                    localStorage.setItem('itemsJson', JSON.stringify(itemJsonArray))
                }
                update();
            }

            function update(){
                if (localStorage.getItem('itemsJson')==null){
                    itemJsonArray = []; 
                    localStorage.setItem('itemsJson', JSON.stringify(itemJsonArray))
                } 
                else{
                    itemJsonArrayStr = localStorage.getItem('itemsJson')
                    itemJsonArray = JSON.parse(itemJsonArrayStr); 
                }
                // Populate the table
                let tableBody = document.getElementById("tableBody");
                let str = "";
                itemJsonArray.forEach((element, index) => {
                    str += `
                    <tr>
                    <th scope="row">${index + 1}</th>
                    <td>${element[0]}</td>
                    <td>${element[1]}</td> 
                    <td><button class="btn btn-sm btn-dark" onclick="deleted(${index})">Delete</button></td> 
                    </tr>`; 
                });
                tableBody.innerHTML = str;
            }
            add = document.getElementById("add");
            add.addEventListener("click", getAndUpdate);
            update();
            function deleted(itemIndex){
                console.log("Delete", itemIndex);
                itemJsonArrayStr = localStorage.getItem('itemsJson')
                itemJsonArray = JSON.parse(itemJsonArrayStr);
                // Delete itemIndex element from the array
                itemJsonArray.splice(itemIndex, 1);
                localStorage.setItem('itemsJson', JSON.stringify(itemJsonArray));
                update();

            }
            function clearStorage(){
                if (confirm("Are you sure you want to clear the list??")){
                console.log('Clearing the storage')
                localStorage.clear();
                update()
                }
            }
        </script>
</body>

</html>
