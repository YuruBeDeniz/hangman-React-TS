# hangman-React-TS
we need to track 2 states:
1. word to guess
2. guessed letters
easiest way to do that is to store them in an array

### styling
we cant do hover or focus in react so we need to use CSS file for that.

### useEffect
in order to hook up an event listener for our actual keyboard
(not the visual keyboard) we need to use useEffect
Then, add an event listener for key press and on this key press, we need to call handler function
Then, make sure to clean this up and remove this event listener whenever our use event is done working (like when our component is removed) so we can remove our event listener or key press and we can make sure that we remove that handle function we created
(inside useEffect: handler function is our event listener, and the rest is just hooking it up (document.addEventListener("keypress", handler)) and removing it (return () => {document.removeEventListener("keypress", handler)}))

if the key is pressed; add it to guessed letters: addGuessedLetter(key);
if we guess the same letter twice, we shouldnt be punished for, so: 
if(guessedLetters.includes(letter)) return;
otherwise;
return all those current letters and add our letter to the end of that array:
setGuessedLetters(currentLetters => [...currentLetters, letter])

we only want useEffect function rerun when the thing inside of it change for example our guessedLetters change. So in order to change that we can use a useCallback:
update the addGuessedLetter function as:
const addGuessedLetter = useCallback((letter: string) => {
      if (guessedLetters.includes(letter)) return;

      setGuessedLetters(currentLetters => [...currentLetters, letter])
    },
    [guessedLetters])
we need to pass in different dependencies inside the array at the end of the useCallback function. Our guessedLetters are the only thing this function depends on (for now) so every time that changes we are going to rerun our function. addGuessedLetters function only changes every time our guessedLetter changes, so if you press the same key it won't change.

for ref: https://github.com/WebDevSimplified/react-hangman