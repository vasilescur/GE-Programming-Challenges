# Week 1

## [Easy] Perfectly Balanced, as All Things Should Be (1 point)

Given a string containing only the characters `x` and `y`, find whether there are the same number of `x`’s and `y`’s. 
Input: string, output: boolean or truthy/falsy value.

Test Cases:
```
balanced("xxxyyy") => true
balanced("yyyxxx") => true
balanced("xxxyyyy") => false
balanced("yyxyxxyxxyyyyxxxyxyx") => true
balanced("xyxxxxyyyxyxxyxxyy") => false
balanced("") => true
balanced("x") => false
```

### Reference Implementation

```py
def balanced(word):
  return word.count('x') == word.count('y')
```

### Featured Solutions

```clojure
(defn balanced [letters] 
    (let [freqs (frequencies (char-array letters))]
        (= (get freqs \x) (get freqs \y))))
```

```java
public static Boolean balanced(String input)
{
   int counterX = 0;

   for(int i = 0; i < input.length(); i++)
   {
      if(input.charAt(i) == 'x')
      {
          counterX++;
      }
      if(input.charAt(i) == 'y')
      {
          counterX--;
      }
   }

   if(counterX == 0)
   {
      return true;
   }
   return false;
}
```

## [Hard] What Time is It? (3 points)

Given the time in numbers, output the time in text. This is using 24 hour time (0:00 – 23:59). 
Input: string, output: string.

Test Cases:
```
timeString("00:00") => "It's twelve am"
timeString("01:30") => "It's one thirty am"
timeString("12:05") => "It's twelve o five pm"
timeString("14:01") => "It's two o one pm"
timeString("20:29") => "It's eight twenty nine pm"
timeString("21:00") => "It's nine pm"
```

### Reference Implementation

```clojure
;; num-to-eng :: int -> string
(defn num-to-eng [num]
    "Converts an integer to English. Uses the handy Common Lisp `format` with \"~r\"."
    (clojure.string/replace 
        (clojure.pprint/cl-format nil "~r" num) 
        "-" 
        " "))

;; time-eng :: string -> string
(defn time-eng [timestamp]
    "Converts an hh:mm timestamp to English 12-hour notation."
    (let [parts (clojure.string/split timestamp #":")]
        (let [hour-num (read-string (get parts 0))] 
            (let [hour (if (> hour-num 12) 
                            (- hour-num 12) 
                            hour-num)]
            (str
                "It's "
                (if (= (get parts 0) "00") 
                    "twelve" 
                    (num-to-eng hour))
                " "
                (let [minutes (read-string (get parts 1))
                      minutes-str (num-to-eng minutes)]
                    (cond
                        (= minutes 0) ""
                        (< minutes 10) (str "o " minutes-str " ")
                        :else (str minutes-str " ")))
                (if (> hour-num 12) "pm" "am"))))))

;; main :: nil -> nil
(defn -main []
    "Run the given test cases."
    (let [test-cases 
        '("00:00", "01:30", "12:05", "14:01", "20:29", "21:00")]
        (map (fn [x] (println (time-eng x))) test-cases)))


(-main) ;; Entry point
```

### Featured Solutions

```python
hourwords = {0: 'twelve', 1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five', 6: 'six', 7: 'seven', 8: 'eight', 9: 'nine', 10: 'ten', 11: 'eleven', 12: 'twelve'}
minutewords = {1: 'o one', 2: 'o two', 3: 'o three', 4: 'o four', 5: 'o five', 6: 'o six', 7: 'o seven', 8: 'o eight', 9: 'o nine', 10: 'ten', 11: 'eleven', 12: 'twelve', 13: 'thirteen', 14: 'fourteen', 15: 'fifteen', 16: 'sixteen', 17: 'seventeen', 18: 'eighteen', 19: 'nineteen'}
minutetenswords = {2: 'twenty', 3: 'thirty', 4: 'forty', 5: 'fifty', 6: 'sixty'}
minuteoneswords = {0: '', 1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five', 6: 'six', 7: 'seven', 8: 'eight', 9: 'nine'}

def timeString(time):
  hour = int(time.split(':')[0])
  minute_word = time.split(':')[1]
  minute = int(minute_word)
 
  if hour >= 12: 
    am_or_pm = 'pm'
    hour = hour - 12
  else: 
    am_or_pm = 'am'

  hour_final = hourwords[hour]


  if minute == 0:
    return "It's {} {}".format(hour_final, am_or_pm)
  elif minute < 20: 
    minute_final = minutewords[minute]
  elif int(minute_word[1]) == 0:
    minute_final = minutetenswords[int(minute_word[0])]
  else: 
    minute_final = minutetenswords[int(minute_word[0])] + ' ' + minuteoneswords[int(minute_word[1])]


  return "It's {} {} {}".format(hour_final, minute_final, am_or_pm)
```

```java
private static List<String> dict = Arrays.asList("twelve", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen", "twenty", "twenty one", "twenty two", "twenty three", "twenty four", "twenty five", "twenty six", "twenty seven", "twenty eight", "twenty nine", "thirty", "thirty one", "thirty two", "thirty three", "thirty four", "thirty five", "thirty six", "thirty seven", "thirty eight", "thirty nine", "forty", "forty one", "forty two", "forty three", "forty four", "forty five", "forty six", "forty seven", "forty eight", "forty nine", "fifty", "fifty one", "fifty two", "fifty three", "fifty four", "fifty five", "fifty six", "fifty seven", "fifty eight", "fifty nine");

private static String timeString(String input)
{
  String[] timeArray = input.split(":");
  int hours = Integer.parseInt(timeArray[0]);
  int minutes = Integer.parseInt(timeArray[1]);
  boolean PM = hours > 11;

  return "It's " + (hours > 13 ? numToWord(hours-12) : numToWord(hours)) 
    + (minutes < 10 && minutes != 0 ? " o " : " ") 
    + (minutes == 0 ? "" : numToWord(minutes) + " ") 
    + (PM ? "pm" : "am");
}

private static String numToWord(int input)
{
  return dict.get(input);
}
```

