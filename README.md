const fs = require('fs');
const path = require('path');

// Get the user input for `buicname` dynamically (assuming it's passed as input)
const userInputBuicname = 'sw_accountservices'; // Replace this with actual user input

// Define the old filename and the new filename
const directoryPath = path.join(__dirname, 'files'); // Path to the files directory
const oldFileName = `buicname-element.module.ts`;    // Existing file name
const newFileName = `${userInputBuicname}-element.module.ts`; // New file name with user input

// Full path for the old and new files
const oldFilePath = path.join(directoryPath, oldFileName);
const newFilePath = path.join(directoryPath, newFileName);

// Rename the file
fs.rename(oldFilePath, newFilePath, (err) => {
    if (err) {
        return console.error('Error renaming file:', err);
    }
    console.log(`File renamed from ${oldFileName} to ${newFileName}`);
});
