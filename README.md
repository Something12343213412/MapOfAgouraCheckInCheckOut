# MapOfAgouraCheckInCheckOut
For Student keeps track of where people are and can sign in and out through buttons on a sheet

link to sheet https://docs.google.com/spreadsheets/d/1DhJhv-xQRpDHLRFA-w3xwO_CBHNKt7mY1eUEQmiDsgI/edit#gid=0

var sheet = SpreadsheetApp.getActiveSheet()

function addToList(column = "A",columnTimeStamp = "B", numOfPeople = gNP("C")){
  var ui = SpreadsheetApp.getUi();
  var result = ui.prompt("Enter Your Name for area " + sheet.getRange("Data!" + column + "1").getValue() + "\n leave blank to cancel");
  if(result.getResponseText() != null){
    console.log("Data!" + column + (numOfPeople+2))
    console.log(result.getResponseText())
    sheet.getRange("Data!" + column + (numOfPeople+2)).setValue(result.getResponseText())
    const currentTime = new Date
    sheet.getRange("Data!"+ columnTimeStamp + (numOfPeople+2)).setValue(currentTime.toString().split(" ")[4])
  }
}


// get number of people, just really lazy to write it all out
function gNP(column){
  return sheet.getRange("Data!" + column + "2").getValue()
} 

function addToBuilding() {
  addToList("A", 0)
}

// hate having to do all this manually but don't really see a other way, also too lazy to think of a better way
function aBuilding(){
  addToList("A", "B", gNP("C"))
}

//function 


function bBuilding(){
  addToList("D", "E", gNP("F"))
}

function cBuilding(){
  addToList("G", "H", gNP("I"))
}

function dBuilding(){
  addToList("K", "L", gNP("M"))
}

function eBuilding(){
  addToList("N", "O", gNP("P"))
}

function jBuilding(){
  addToList("Q", "R", gNP("S"))
}

function kBuilding(){
  addToList("T", "U", gNP("V"))
}

function gBuilding(){
  addToList("AI", "AJ", gNP("AK"))
}

function mBuilding(){
  addToList("W", "X", gNP("Y"))
}

function nBuilding(){
  addToList("Z", "AA", gNP("AB"))
}

function rBuilding(){
  addToList("AC", "AD", gNP("AE"))
}

function autoTech(){
  addToList("AF", "AG", gNP("AH"))
}

function vBuilding(){
  addToList("AL", "AM", gNP("AN"))
}

function gymLockerRoomsPool(){
  addToList("AO", "AP", gNP("AQ"))
}

function softBallBaseBall(){
  addToList("AR", "AS", gNP("AT"))
}

function tenisCourtsWeight(){
  addToList("AU", "AV", gNP("AW"))
}

function pAC(){
  addToList("AX", "AY", gNP("AZ"))
}

function soccerField(){
  addToList("BA", "BB", gNP("BC"))
}

function track(){
  addToList("BD", "BE", gNP("BF"))
}

function mainQuad(){
  addToList("BG", "BH", gNP("BI"))
}

function lBuilding(){
  addToList("BJ", "BK", gNP("BL"))
}


function clearData(){
  var ui = SpreadsheetApp.getUi();
  var password = ui.prompt("What is the password")
  if (password.getResponseText() == "A"){
    sheet.getRange("Data!A1:BL50").setValues(sheet.getRange("Data 2, Don't mess with, ignore!A1:BL50").getValues())
    ui.alert("Right Password, all data deleted")
  }
  else
    ui.alert("Wrong Password")

  fixFunctions()
}

// needed bc I am lazy and don't feel like writing proper code
function autoClearFunction(){
  sheet.getRange("Data!A1:BL50").setValues(sheet.getRange("Data 2, Don't mess with, ignore!A1:BL50").getValues())
  fixFunctions()
}



function printAllNames(){
  var ui = SpreadsheetApp.getUi();
  var range = sheet.getRange("Data!A1:BL50").getValues()
  var people = []
  // loops through all of the top row
  for (var a = 0; a < range[0].length; a++){
    // checks if the range is neither checking time or the number of people
    if (range[0][a] != "TimeStamp" && range[0][a] != "Num Of People"){
      for(var y = 1; y < range.length; y++){
        if (range[y][a])
          people.push(" | " + range[0][a] + ": " + range[y][a])
      }
    }
  }
  ui.alert(people.toString());
}


function testing(){
  var ui = SpreadsheetApp.getUi();
  var range = sheet.getRange("Data!A1:BL100").getValues()
  var person = "2023"
  var haveRemoved = false;

  if (!person == ""){
    for (var y = 1; y < 15; y++){
      range[y] = range[y].toString()
      range[y] = range[y].split(",")
      index = range[y].indexOf(person)
      if (index != -1){
        range[y][index] = ""
        range[y][index+1] = ""
        ui.alert(person + " removed from " + range[0][index])
        haveRemoved = true
        console.log(index)
      }
      
      for (var x = y; x < 15; x++)
        range[y+x][index] = range[y+x+1][index] 
      
      
    }
    if (!haveRemoved)
      ui.alert("The name you entered was not in the sheet")
  }
}

function removeName(){
  var ui = SpreadsheetApp.getUi();
  var range = sheet.getRange("Data!A1:BL100").getValues()
  var person = ui.prompt("What is your name? Leave blank to cancel").getResponseText()
  
  var index;
  var haveRemoved = false

  if (!person == ""){
    for (var y = 1; y < 15; y++){
      // converting range to string and back to make sure any int values are now strings
      range[y] = range[y].toString()
      range[y] = range[y].split(",")

      // getting index of the person in the given row, if none don't run the code to change the person
      index = range[y].indexOf(person)
      if (index != -1){
        range[y][index] = ""
        range[y][index+1] = ""
        ui.alert(person + " removed from " + range[0][index])
        haveRemoved = true
      }
      
      // moves down a row
      for (var x = y; x < 15; x++)
        range[y+x][index] = range[y+x+1][index] 
      
      
    }
    if (!haveRemoved){
      ui.alert("The name you entered was not in the sheet")
      return -1
    }
  }

  sheet.getRange("Data!A1:BL100").setValues(range)
  fixFunctions();
}

// lazy but really hate this solution
function fixFunctions(){
  sheet.getRange("Data!C2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!C2").getFormula())
  sheet.getRange("Data!F2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!F2").getFormula())
  sheet.getRange("Data!I2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!I2").getFormula())
  sheet.getRange("Data!M2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!M2").getFormula())
  sheet.getRange("Data!P2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!P2").getFormula())
  sheet.getRange("Data!S2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!S2").getFormula())
  sheet.getRange("Data!V2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!V2").getFormula())
  sheet.getRange("Data!Y2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!Y2").getFormula())
  sheet.getRange("Data!AB2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AB2").getFormula())
  sheet.getRange("Data!AE2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AE2").getFormula())
  sheet.getRange("Data!AH2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AH2").getFormula())
  sheet.getRange("Data!AK2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AK2").getFormula())
  sheet.getRange("Data!AN2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AN2").getFormula())
  sheet.getRange("Data!AQ2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AQ2").getFormula())
  sheet.getRange("Data!AT2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AT2").getFormula())
  sheet.getRange("Data!AW2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AW2").getFormula())
  sheet.getRange("Data!AZ2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!AZ2").getFormula())
  sheet.getRange("Data!BC2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!BC2").getFormula())
  sheet.getRange("Data!BF2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!BF2").getFormula())
  sheet.getRange("Data!BI2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!BI2").getFormula())
  sheet.getRange("Data!BL2").setFormula(sheet.getRange("Data 2, Don't mess with, ignore!BL2").getFormula())

}

function test(){
  
  var range = sheet.getRange("Data!A1:BL100").getValues()

  for (var y = 1; y < 50; y++){
    index = range[y].indexOf("Dani, London, Alex")
    if (index != -1){
      range[y][index] = ""
      range[y][index+1] = ""
      console.log(range[y][index])
      haveRemoved = true
      for (var x = 0; x < 50; x++)
        range[y+x][index] = range[y+x+1][index]
    }
    
           
  }
  
  sheet.getRange("Data!A1:BL100").setValues(range)
  fixFunctions();
}
