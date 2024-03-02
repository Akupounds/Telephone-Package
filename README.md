# Telephone Package
 A telephone package that aloows yo to AddPhoneNumber, RemovePhoneNumber and DialPhoneNumber
const readline = require('readline');

class Telephone {
  constructor() {
    this.phoneNumbers = new Set();
  }

  // Method to add a new phone number
  addPhoneNumber(number) {
    this.phoneNumbers.add(number);
    console.log(`Added ${number} to the phone book.`);
  }

  // Method to remove a phone number
  removePhoneNumber(number) {
    if (this.phoneNumbers.has(number)) {
      this.phoneNumbers.delete(number);
      console.log(`Removed ${number} from the phone book.`);
    } else {
      console.log(`${number} is not in the phone book.`);
    }
  }

  // Method to dial a phone number
  dialPhoneNumber(number) {
    if (this.phoneNumbers.has(number)) {
      console.log(`Dialing ${number}...`);
    } else {
      console.log(`${number} is not in the phone book. Add the number before dialing.`);
    }
  }
}

// Function to get user input
function getUserInput(question) {
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
  });

  return new Promise((resolve) => {
    rl.question(question, (answer) => {
      resolve(answer);
      rl.close();
    });
  });
}

// Example usage with user input
(async () => {
  const myTelephone = new Telephone();

  while (true) {
    console.log('\n1. Add Phone Number\n2. Remove Phone Number\n3. Dial Phone Number\n4. Exit');
    const choice = await getUserInput('Enter your choice (1-4): ');

    switch (choice) {
      case '1':
        const newNumber = await getUserInput('Enter the phone number to add: ');
        myTelephone.addPhoneNumber(newNumber);
        break;

      case '2':
        const removeNumber = await getUserInput('Enter the phone number to remove: ');
        myTelephone.removePhoneNumber(removeNumber);
        break;

      case '3':
        const dialNumber = await getUserInput('Enter the phone number to dial: ');
        myTelephone.dialPhoneNumber(dialNumber);
        break;

      case '4':
        console.log('Exiting...');
        process.exit(0);

      default:
        console.log('Invalid choice. Please enter a number between 1 and 4.');
    }
  }
})();


