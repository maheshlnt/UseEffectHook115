# UseEffectHook115
Useeffect for forms: runs when any changes occured. to avoid dataleaks use return for clearing data.


In LOGIN PAGE:

const Login = (props) => {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [emailIsValid, setEmailIsValid] = useState();
  const [enteredPassword, setEnteredPassword] = useState('');
  const [passwordIsValid, setPasswordIsValid] = useState();
  const [formIsValid, setFormIsValid] = useState(false);


useEffect(()=>{
const identifier= setTimeout(()=>{
  console.log('checking validity');//After 500milliseconds this line/code runs, pausing typing more than 500millis
  setFormIsValid(
    enteredEmail.includes('@') && enteredPassword.trim().length > 6
  );
},500);
return ()=>{    // return statement used for cleaning all previous onkey up data. update with new keyup data. to avoid dataleaks
  console.log("cleanup");
  clearTimeout(identifier);
}
},[enteredEmail, enteredPassword]);


In APP.JS
function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

useEffect(()=>{
  const storedLocalStorage=localStorage.getItem('isLoggedIn');
  if(storedLocalStorage==="1"){
    setIsLoggedIn(true);
  }
},[]);
  const loginHandler = (email, password) => {
    // We should of course check email and password
    // But it's just a dummy/ demo anyways
    localStorage.setItem('isLoggedIn','1');
    setIsLoggedIn(true);
  };
 
  const logoutHandler = () => {
    localStorage.setItem('isLoggedIn','0');
    setIsLoggedIn(false);
  };
