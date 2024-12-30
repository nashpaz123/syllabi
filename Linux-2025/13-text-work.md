# מניפולציית טקסט בלינוקס - מדריך מקיף

## כלים בסיסיים

### הצגת תוכן קבצים

#### פקודת cat
```bash
# הצגת תוכן קובץ
cat file.txt

# הצגת מספרי שורות
cat -n file.txt

# הצגה עם סימון שורות ריקות
cat -b file.txt

# שרשור מספר קבצים
cat file1.txt file2.txt > combined.txt
```

#### פקודת less
```bash
# הצגת תוכן עם גלילה
less file.txt

# חיפוש בתוך less:
/מילה        # חיפוש קדימה
?מילה        # חיפוש אחורה
n           # תוצאה הבאה
N           # תוצאה קודמת
q           # יציאה
```

#### פקודת head ו-tail
```bash
# הצגת 10 השורות הראשונות
head file.txt

# הצגת 5 השורות הראשונות
head -n 5 file.txt

# הצגת 10 השורות האחרונות
tail file.txt

# מעקב אחרי קובץ בזמן אמת
tail -f log.txt
```

## עיבוד טקסט בסיסי

### מיון עם sort
```bash
# מיון בסיסי
sort file.txt

# מיון מספרי
sort -n numbers.txt

# מיון הפוך
sort -r file.txt

# מיון לפי עמודה ספציפית
sort -k2 data.txt

# מיון ייחודי (הסרת כפילויות)
sort -u file.txt
```

### ספירה עם wc
```bash
# ספירת שורות, מילים ותווים
wc file.txt

# ספירת שורות בלבד
wc -l file.txt

# ספירת מילים בלבד
wc -w file.txt

# ספירת תווים בלבד
wc -m file.txt
```

### שימוש ב-uniq
```bash
# הסרת שורות כפולות (חייב להיות ממוין)
sort file.txt | uniq

# ספירת כמה פעמים מופיעה כל שורה
sort file.txt | uniq -c

# הצגת רק שורות שמופיעות יותר מפעם אחת
sort file.txt | uniq -d
```

## עיבוד טקסט מתקדם

### שימוש ב-sed
```bash
# החלפת טקסט
sed 's/ישן/חדש/' file.txt        # החלפה ראשונה בכל שורה
sed 's/ישן/חדש/g' file.txt       # החלפת כל המופעים
sed -i 's/ישן/חדש/g' file.txt    # החלפה בקובץ עצמו

# מחיקת שורות
sed '3d' file.txt                # מחיקת שורה 3
sed '/pattern/d' file.txt        # מחיקת שורות שמכילות תבנית

# הוספת טקסט
sed '2i\טקסט חדש' file.txt      # הוספה לפני שורה 2
sed '2a\טקסט חדש' file.txt      # הוספה אחרי שורה 2

# עבודה עם טווחים
sed '2,5d' file.txt             # מחיקת שורות 2-5
sed '2,5s/ישן/חדש/g' file.txt    # החלפה בשורות 2-5
```

### שימוש ב-awk
```bash
# הדפסת עמודות ספציפיות
awk '{print $1}' file.txt         # הדפסת העמודה הראשונה
awk '{print $1,$3}' file.txt      # הדפסת עמודות 1 ו-3

# פעולות חשבון
awk '{sum += $1} END {print sum}' file.txt     # סכום העמודה הראשונה
awk '{sum += $1} END {print sum/NR}' file.txt  # ממוצע העמודה הראשונה

# סינון שורות
awk '$1 > 100' file.txt          # שורות שהערך הראשון גדול מ-100
awk 'NR > 10' file.txt           # שורות אחרי שורה 10

# עיבוד מתקדם
awk '
    BEGIN {print "התחלה"}        # פעולות לפני העיבוד
    {
        if ($1 > 100) {          # תנאים
            count++
            total += $1
        }
    }
    END {                        # פעולות בסוף העיבוד
        print "סהכ:", count
        print "ממוצע:", total/count
    }
' file.txt
```

## השוואת קבצים

### פקודת diff
```bash
# השוואה בסיסית
diff file1.txt file2.txt

# השוואה בפורמט תמציתי
diff -y file1.txt file2.txt

# השוואה בפורמט מאוחד
diff -u file1.txt file2.txt

# התעלמות מרווחים
diff -w file1.txt file2.txt
```

### פקודת comm
```bash
# השוואת קבצים ממוינים
comm file1.txt file2.txt

# הצגת שורות ייחודיות לקובץ הראשון
comm -23 file1.txt file2.txt

# הצגת שורות משותפות
comm -12 file1.txt file2.txt
```

## טיפים וטריקים

### שרשור פקודות
```bash
# שימוש ב-pipe
cat file.txt | grep "מילה" | sort | uniq

# סינון וספירה
grep "שגיאה" log.txt | wc -l

# עיבוד מורכב
cat data.txt | 
    awk '{print $2,$1}' |        # החלפת סדר העמודות
    sort -k1 |                   # מיון לפי העמודה הראשונה
    uniq -c |                    # ספירת כפילויות
    sort -nr                     # מיון מספרי הפוך
```

### דוגמאות שימושיות
```bash
# מציאת קבצים הכי גדולים בתיקייה
du -h | sort -hr | head -n 10

# חיפוש שורות כפולות
sort file.txt | uniq -d

# מציאת IP הכי פעילות בלוג
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head

# החלפת מחרוזות בכל הקבצים
find . -type f -name "*.txt" -exec sed -i 's/ישן/חדש/g' {} +
```

## פתרון בעיות נפוצות

### בעיות קידוד
```bash
# המרת קידוד
iconv -f ISO-8859-8 -t UTF-8 file.txt > newfile.txt

# בדיקת סוג קידוד
file -i file.txt
```

### עבודה עם קבצים גדולים
```bash
# חיפוש יעיל
grep --line-buffered "pattern" bigfile.txt | less

# עיבוד בחלקים
split -l 1000 bigfile.txt part_
for f in part_*; do
    process_file "$f"
done
```
