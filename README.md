# Step-3-Publish-Reflect
const fs = require('fs');

const readline = require('readline');

const outputFile = ProcessingInstruction.argv[2];

if (!outputFile) {
  console.error('Error: Please provide an output file path.');
  console.log('Usage: node fancyTee.js <outputFile>');
  process.exit(1);
}

const rl = readline.createInterface ({
  input: process.stdin,
  output: process.stdout,
  terminal: false
});

const timestamp = new Date().toISOString();
const logStream = fs.createWriteStream(outputFile, { flags: 'w' });

logStream.write(`--- Log Created: ${timestamp} ---\n`);

let lineNum = 1;

rl.on('line', (line) => {
  logStream.write(`[Line ${lineNume} ${line}\n]`);
  lineNum++;
});

rl.on('close', () => {
  logStream.write(`--- End of Log (${lineNum - 1} lines recorded) ---\n`);
  logStream.end();

}); 

