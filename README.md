const fs = require('fs');
const readline = require('readline');

// Function to read file and replace text
async function replaceInFile(filePath, searchValue, replaceValue) {
  try {
    // Read the file content
    const data = fs.readFileSync(filePath, 'utf8');

    // Replace all occurrences of searchValue with replaceValue
    const result = data.replace(new RegExp(searchValue, 'g'), replaceValue);

    // Write the modified content back to the file
    fs.writeFileSync(filePath, result, 'utf8');

    console.log(`Replaced "${searchValue}" with "${replaceValue}" in ${filePath}`);
  } catch (err) {
    console.error(`Error reading or writing file: ${err}`);
  }
}

// Function to prompt user for input
async function promptUser(query) {
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });

  return new Promise((resolve) => rl.question(query, (answer) => {
    rl.close();
    resolve(answer);
  }));
}

// Main function to run the script
async function main() {
  // Get the BUIC name from the user
  const buicName = await promptUser('Enter the BUIC name: ');

  // Path to the angular.json file
  const filePath = './files/angular.json';

  // Replace the specified text in the file
  replaceInFile(filePath, 'cct-synergyweb-powerofattorney', buicName);
}

// Run the main function
main();
