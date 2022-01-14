# Cookies

## Accessed and set by

```
document.cookie = 'name=Kyle';
```

By default the experation date of cookies is set way back in the past (1969) to set an experation date:

```
const tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);
document.cookie = 'name=Kyle; expires=' + tomorrow.toUTCString();
```

To never expire use a very far date

## Read Cookies:

```
const cookies = document.cookie
```
