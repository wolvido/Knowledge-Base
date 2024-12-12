Front-end validation (javascript) can easily be bypassed. It should only be used to improve the "user experience" - by providing instant feedback. It also reduces the load on the server.

Back-end validation is a MUST. It has to ensure that the data coming in is indeed valid. Additionally, depending on your architecture, you generally re-use your middle-tier business logic amongst multiple components so you need to ensure the rules that are applied are always consistent - regardless of what the front-end logic enforces.

according to stack overflower
[Should I handle html form validation on front or backend? - Stack Overflow](https://stackoverflow.com/questions/37492271/should-i-handle-html-form-validation-on-front-or-backend)