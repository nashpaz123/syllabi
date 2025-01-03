# תהליכים בלינוקס - מדריך מעמיק

## מה זה תהליך?
תהליך הוא תוכנית שרצה במחשב. כל תהליך בלינוקס מקבל מספר מזהה ייחודי שנקרא PID (Process ID). 

### איך המערכת מנהלת תהליכים
- כל תהליך מקבל חלק מזיכרון המחשב
- לכל תהליך יש בעלים (משתמש שהפעיל אותו)
- תהליכים יכולים להיות:
  - תהליכי מערכת (דימונים)
  - תהליכי משתמש
  - תהליכי חזית (שמחוברים למסוף)
  - תהליכי רקע

## כלים לניהול תהליכים

### הפקודה ps
הפקודה הבסיסית לראות תהליכים שרצים במערכת.

דוגמאות שימושיות:
```bash
# להציג את כל התהליכים שלך
ps

# להציג את כל התהליכים במערכת
ps aux

# להציג תהליכים בפורמט עץ
ps axjf

# לחפש תהליך ספציפי
ps aux | grep firefox
```

פירוש השדות ב-ps:
- PID: מספר התהליך
- TTY: המסוף שממנו רץ התהליך
- STAT: מצב התהליך (R=רץ, S=ישן, Z=זומבי)
- TIME: זמן המעבד שהתהליך ניצל
- COMMAND: שם התוכנית

### השימוש ב-top
top היא פקודה שמציגה תהליכים בזמן אמת.

פקודות שימושיות בתוך top:
- k: להרוג תהליך
- r: לשנות עדיפות
- h: עזרה
- q: לצאת

דוגמה לפלט של top:
```
top - 14:28:48 up  1:15,  1 user,  load average: 0.52, 0.58, 0.59
Tasks: 266 total,   1 running, 265 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.9 us,  1.6 sy,  0.0 ni, 92.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  15867.7 total,   9098.9 free,   3209.7 used,   3559.1 buff/cache
```

### הריגת תהליכים
יש כמה דרכים להרוג תהליכים:

```bash
# הריגה רגילה
kill 1234

# הריגה מיידית
kill -9 1234

# הריגה לפי שם
killall firefox

# הריגה עדינה
kill -15 1234
```

סוגי סיגנלים נפוצים:
- SIGTERM (15): בקשה מנומסת לסיים
- SIGKILL (9): סיום מיידי
- SIGHUP (1): איתחול מחדש
- SIGSTOP (19): השהייה

### עדיפויות תהליכים
לינוקס מאפשרת לקבוע עדיפויות לתהליכים:

```bash
# הפעלת תוכנית בעדיפות נמוכה
nice -n 19 command

# שינוי עדיפות לתהליך קיים
renice +5 -p 1234
```

ערכי עדיפות:
- -20 עד 19
- ככל שהמספר נמוך יותר, העדיפות גבוהה יותר
- משתמש רגיל יכול רק להוריד עדיפות

## עבודה עם תהליכי רקע וחזית

### העברת תהליכים לרקע
```bash
# הפעלה ישירה ברקע
command &

# העברה לרקע תוך כדי ריצה
[Ctrl+Z] להשהות
bg להעביר לרקע
```

### החזרת תהליכים לחזית
```bash
# החזרת התהליך האחרון
fg

# החזרת תהליך ספציפי
fg %1
```

### ניהול משימות
```bash
# הצגת כל המשימות
jobs

# הצגת מספרי המשימות
jobs -l
```

## דוגמאות מעשיות

### תסריט לניטור זיכרון
```bash
watch -n 5 'free -m'
```

### מציאת תהליכים שצורכים הרבה זיכרון
```bash
ps aux --sort=-%mem | head
```

### הפעלת תהליך שימשיך גם אחרי התנתקות
```bash
nohup command &
```

### בדיקת משאבים של תהליך ספציפי
```bash
top -p 1234
```

## טיפים מתקדמים

### שימוש ב-htop
htop הוא כלי משופר לניהול תהליכים:
- תצוגה צבעונית
- עכבר עובד
- תמיכה בגלילה
- מיון לפי כל עמודה

### ניטור תהליכים עם atop
atop שומר היסטוריה של פעילות המערכת:
- מראה שימוש במשאבים לאורך זמן
- שומר נתונים לניתוח מאוחר יותר
- מציג מידע על דיסק ורשת

### הגבלת משאבים עם ulimit
```bash
# הגבלת זיכרון
ulimit -v 1000000

# הגבלת מספר קבצים
ulimit -n 1000
```

## פתרון בעיות נפוצות

### תהליך תקוע
1. נסו קודם SIGTERM
2. אם לא עוזר, השתמשו ב-SIGKILL
3. בדקו אם יש תהליכי ילד

### צריכת משאבים גבוהה
1. השתמשו ב-top לזיהוי התהליך
2. בדקו לוגים
3. שקלו להוריד עדיפות

### תהליכי זומבי
- תהליכים שסיימו לרוץ אבל עדיין בטבלת התהליכים
- בדרך כלל לא מזיקים
- אפשר להיפטר מהם על ידי איתחול מחדש של תהליך האב
