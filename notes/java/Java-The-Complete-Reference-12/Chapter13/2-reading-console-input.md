# Reading Console Input

> for commercial applications, the preferred method of reading console input is to use a **character-oriented** stream.
> this makes your program easier to internationalize and maintain

> before JDK17

```java
   InputStreamReader inputStreamReader = new InputStreamReader(System.in);
   BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
```

> after JDK17, recomment explicitly sepcify the **charset**

```java
   Console console = System.console();
   InputStreamReader inputStreamReader2 = new InputStreamReader(System.in, console.charset());
   BufferedReader bufferedReader2 = new BufferedReader(inputStreamReader2);
```

## reading characters

> `BufferedReader.read()`
- it reads a character from the input stream, and returns it as an integer value.
- it returns -1 when an attempt is made to read at the end of the stream.
- **System.in** is line buffered, by default.
- this means that no input is actually passed to the program until you press enter.

```java
BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in, System.console().charset()));
char c = 0;
do {
try {
    c = (char)bufferedReader.read();
} catch (IOException e) {
    e.printStackTrace();
}
} while (c != 'q');
```

## reading strings

> `BufferedReader.readLine()`

```java
    BufferedReader bufferedReader =
        new BufferedReader(new InputStreamReader(System.in, System.console().charset()));
    String s = null;
    do {
      try {
        s = bufferedReader.readLine();
      } catch (IOException e) {
        e.printStackTrace();
      }
    } while (!s.equals("stop"));
  }
```

## Writing Console Output
> `PrintStream.write(int byteval)`
```java
int b = 'A';
System.out.write(b);
```
> although bytevalue is declared as an integer, **only the low-order eight bits are written**
