# Digesting API data using Google App Script and printing on sheet.

 **1. Create a fresh google sheet file**
- on tools click edit script

**2. On the appscript write the script to digest the data**

```
function myFunction() {
  var url ="https://randomuser.me/api" //define your API of choice 
  var response = UrlFetchApp.fetch(url)
  var data = response.getContentText()
  var result = JSON.parse(data)

//variable parameters to be appended on sheet
  var email = result.results[0].email
  var username = result.results[0].login.username
  var password = result.results[0].login.password
  var picture = result.results[0].picture.large



var sheet = SpreadsheetApp.getActiveSheet()

sheet.clear() // clear initial prints


//organize your rows
var headRow = ['Email', 'Username','Password','Picture']
sheet.appendRow(headRow)
var row  = [email,username,password,picture]
sheet.appendRow(row)

// for loop to continously prints the data
for(var i=0; i<result.results.length; i++){
  var row = [result.results[i].email,result.results[i].login.username,result.results[i].login.password,result.results[i].picture.large]
  SpreadsheetApp.getActiveSheet().appendRow(row)


}

}
```