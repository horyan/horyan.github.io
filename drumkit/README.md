js drum kit README.md

<script>
// 1. focus on listening for keyup event
// get whatever element you're listening for.. in our case, listening on: window
// sometimes might wanna listen to input or div or text area
  window.addEventListener('keydown', function (e) {
    console.log(e);
});
// listen for the keydown event and when that happens: we run this function
// which will give us the event
// open up the console: press keys and see KeyboardEvent(s)
// that's what the e is, just the object full of data describing what happened
// (it tells us a lot of info, but we only care about keyCode)
</script>

<script>
  window.addEventListener('keydown', function (e) {
    console.log(e.keyCode);
});
</script>

//is there an audio element on this page that has a data-key of 65
<script>
  window.addEventListener('keydown', function (e) {
      //select an audio element
    const audio = document.querySelector(`audio[data-key=${e.keyCode}]`);
    //querySelector for 1, querySelectorAll for many...attribute selector syntax: audio['data-key=65']
    //attribute selector: use backticks for variable (es6 template strings: "${}") remember single/double quotes!!
    console.log(audio);
    //see if we've selected an actual audio element
    //press q and get null: no audio element associated with 81
});
</script>

<script>
  window.addEventListener('keydown', function (e) {
    const audio = document.querySelector(`audio[data-key=${e.keyCode}]`);
    if (!audio) return; // stop function from running altogether
    audio.play(); //since we have audio element, we can play it
    //works..kind of...hit 'f' multiple times but only plays every so //often.. (openhat takes ~2-3 seconds to finish)
    //when u call .play on an audio element that is already playing,
    //it won't play again
    //rewind it to the start of the element, so we can hit in succession
});
</script>

<script>
  window.addEventListener('keydown', function (e) {
    const audio = document.querySelector(`audio[data-key=${e.keyCode}]`);
    if (!audio) return;
    audio.currentTime = 0;
    //rewind it to the start of the element, so we can hit in succession
    audio.play();
});
</script>
//8:29 of the video

<script>
window.addEventListener('keydown', function (e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  //select the corresponding key - to add animation (instead of audio element, select div or .key - class of key w/ data)
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  if (!audio) return;
  audio.currentTime = 0;
  audio.play();
  console.log(key); //actual key element
});
</script>

<script>
window.addEventListener('keydown', function (e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  if (!audio) return;
  audio.currentTime = 0;
  audio.play();
  key.classList.add('playing'); // vailla JS instead of jQuery equivalent: key.addClass('playing'); - we also we .remove and .toggle (allow you add and remove different classes that you want?)
  //adding but not removing - maybe add setTimeout? but conficts of timeouts here and in the transition (css) - will get out of sync potentially if they aren't lined up
  // use transition end event - fire when thing has stopped animating itself
  // clickevent - fire off event - somebody clicked me, also have events for i didn't get clicked but transitioned myself - so listen on each key for when the transition event happens
});
// select every key on this page to listen for it on each one
const keys = document.querySelectorAll('.key')
// running in console gives us an array of every single element that is matched - good
// listen for an event called transitionEnd on each one
//cannot just do keys.addEventListener('transactionend'); bc problem = when u have an array of elements u cannot listen on all of them, u must explicitly loop over every single element and attach an event listener
keys.forEach(key => key.addEventListener('transitionend', removeTransition);) //ES6 arow function -- each key gets a eventListener added to it which is transitionend, when a transition is ending, remove it -- now we write a function...
</script>

<script>
window.addEventListener('keydown', function (e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  if (!audio) return;
  audio.currentTime = 0;
  audio.play();
  key.classList.add('playing');
});

//that will give us the event, and inside of that - just console.log the event to see what we are working with
function removeTransition(e) {
  console.log(e)
}
// press 'a' = 6 transactioneend events for that one little fade in where it got a little bit bigger - that's because a whole bunch of things transitioned here: border-right-color transitioned (...all of the borders have transitioned), the box-shadow (that little yellow glow has transitioned), and also the transform has fiinished - which we don't care about all - just really do it when 1 thing is over, generally the longest one - pick transform

const keys = document.querySelectorAll('.key')
keys.forEach(key => key.addEventListener('transitionend', removeTransition));

</script>

<script>
window.addEventListener('keydown', function (e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  if (!audio) return;
  audio.currentTime = 0;
  audio.play();
  key.classList.add('playing');
});

//[we got this function that will run when a transaction has ended]this will give us the event, and inside of that - just console.log the event to see what we are working with
function removeTransition(e) {
  if(e.propertyName !== 'transform') return; // skip it if it's not a transform
  //what's next? let's just
  console.log(e.propertyName);
  //it's console logging the word transform bc that is the property that is being ended
}

const keys = document.querySelectorAll('.key')
keys.forEach(key => key.addEventListener('transitionend', removeTransition));

</script>

//just the function
<script>
function removeTransition(e) {
  if(e.propertyName !== 'transform') return;
  this.classList.remove('playing'); //what is this? console.log(this); will tell u - always equal to whatever got called against it (key in this case) (key.addEventListener)
}
</script>

//last thing: mentor is not a big fan of attaching functions right to the keydown so put in own function
<script>
  
  function playSound (e) {
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
    if (!audio) return; // stop function from running
    audio.currentTime = 0; // rewind to the start
    audio.play();
    key.classList.add('playing');
  }

  function removeTransition(e) {
    if (e.propertyName !== 'transform') return; // skip if not a transform
    this.classList.remove('playing');
  }

  const keys = document.querySelectorAll('.key')
  keys.forEach(key => key.addEventListener('transitionend', removeTransition));
  window.addEventListener('keydown', playSound);

</script>

//still works fine, nice and separate, if we ever wanted to play the sound based off of sometheing else- we can
//what we learned:
key events
playing audio
listening for transitionend event
if dealing with animations - can listen for animation end event
