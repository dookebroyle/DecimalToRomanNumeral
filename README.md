# DecimalToRomanNumeral
For the FreeCodeCamp JavaScript programming challenge
function convertToRoman(num) {
  //chart with corresponding indices
  let roman = ['I',"IV","V","IX","X","XL","L","XC","C", "CD", "D", "CM", "M"];
  let eng   = [1,     4,  5,   9, 10,  40, 50, 90, 100,  400, 500,  900,1000];
  let newArr   = [];
  num = num.toString();
  //split to work with each number individually and then change back from string
  num = num.split('').map((i) => { return Number(i); });
  //console.log(num);

  

  
  //need to account for what place(base 10)the digit is in as we step through num array
  let tensPlace = Math.pow(10,(num.length -1)); 
  for (let i = 0; i<num.length; i++){
    while(num[i]>0){
      //console.log(num[i]);
      // find the largest number in eng that the number can fit into
      let index = findEngIndex(num[i]*tensPlace);
      //console.log("Tens Place: " + tensPlace);
      //console.log(index);
      //add the roman numeral to the new array
      newArr.push(roman[index]);
      //decrement the 10's place
      
      //console.log("TensPlace: " + tensPlace + " Loop: " + i);
      //subtract the total num by the amount you added to new array
      num[i] = num[i] - eng[index]/tensPlace;
      //console.log("Equation: " + num[i] + "-" + eng[index] + "/" + tensPlace);
      //console.log(i + "th number: " +num[i]);
    }
    tensPlace = tensPlace/10;
  }
   
  //if you find the eng index the roman index corresponds to it
  function findEngIndex(number){
    for (let j = 0; j<eng.length; j++){
      if(eng[j]> number){
        return j-1;
      }
    }
    //if you haven't found number then its the last index
    return eng.length -1;
  }


 return newArr.join("");
}

convertToRoman(36);
