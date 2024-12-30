# עורכי טקסט בלינוקס - מדריך מקיף

## Vim - עורך טקסט עוצמתי

### התחלת העבודה עם Vim
כדי להתחיל:
```bash
vim filename.txt
```

### מצבי עבודה ב-Vim
1. **מצב פקודה (Normal Mode)**
   - המצב הראשוני כשנכנסים ל-Vim
   - מאפשר ניווט וביצוע פעולות
   
2. **מצב הכנסה (Insert Mode)**
   - נכנסים על ידי לחיצה על `i`
   - מאפשר הקלדת טקסט
   - יוצאים בעזרת `Esc`

3. **מצב חזותי (Visual Mode)**
   - נכנסים על ידי לחיצה על `v`
   - מאפשר בחירת טקסט
   - יוצאים בעזרת `Esc`

### פקודות ניווט בסיסיות
```
h - שמאלה
j - למטה
k - למעלה
l - ימינה
w - מילה קדימה
b - מילה אחורה
0 - תחילת שורה
$ - סוף שורה
gg - תחילת קובץ
G - סוף קובץ
```

### פקודות עריכה נפוצות
```
x - מחיקת תו
dd - מחיקת שורה
yy - העתקת שורה
p - הדבקה אחרי הסמן
P - הדבקה לפני הסמן
u - ביטול פעולה אחרונה
Ctrl+r - ביטול של הביטול
```

### שמירה ויציאה
```
:w - שמירה
:q - יציאה
:wq או ZZ - שמירה ויציאה
:q! - יציאה ללא שמירה
```

### טיפים מתקדמים ל-Vim
- **חיפוש**: 
  ```
  /מילה - חיפוש קדימה
  ?מילה - חיפוש אחורה
  n - תוצאה הבאה
  N - תוצאה קודמת
  ```

- **החלפה**:
  ```
  :%s/ישן/חדש/g - החלפה בכל הקובץ
  :s/ישן/חדש/ - החלפה בשורה הנוכחית
  ```

## Nano - עורך טקסט פשוט וידידותי

### התחלת העבודה
```bash
nano filename.txt
```

### פקודות בסיסיות ב-Nano
```
Ctrl+O - שמירת קובץ
Ctrl+X - יציאה
Ctrl+K - גזירת שורה
Ctrl+U - הדבקת שורה
Ctrl+W - חיפוש טקסט
Ctrl+\ - חיפוש והחלפה
```

### התאמת Nano
קובץ ההגדרות: `~/.nanorc`
```bash
# דוגמאות להגדרות
set linenumbers      # הצגת מספרי שורות
set autoindent       # הזחה אוטומטית
set mouse           # תמיכה בעכבר
set tabsize 4       # גודל טאב
```

## עורכים גרפיים

### Gedit
התקנה:
```bash
sudo apt install gedit
```

תכונות עיקריות:
- תמיכה בתחביר צבעוני
- השלמה אוטומטית
- חיפוש והחלפה מתקדם
- תוספים שימושיים

### Kate
התקנה:
```bash
sudo apt install kate
```

תכונות מרכזיות:
- עריכה במספר לשוניות
- תמיכה בפרויקטים
- הדגשת תחביר
- מסוף מובנה

## תוספים מומלצים

### תוספים ל-Vim
התקנת מנהל התוספים Vundle:
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

תוספים מומלצים:
1. **NERDTree** - סייר קבצים:
   ```
   Plugin 'scrooloose/nerdtree'
   ```

2. **Syntastic** - בדיקת תחביר:
   ```
   Plugin 'vim-syntastic/syntastic'
   ```

3. **YouCompleteMe** - השלמה אוטומטית:
   ```
   Plugin 'ycm-core/YouCompleteMe'
   ```

### תוספים ל-Gedit
1. **Code Comment** - הוספת/הסרת הערות
2. **Word Completion** - השלמת מילים
3. **Terminal** - מסוף מובנה

## טיפים והמלצות

### בחירת עורך טקסט
- **Vim**: למשתמשים מתקדמים שרוצים יעילות מקסימלית
- **Nano**: למתחילים או לעריכה מהירה
- **Gedit/Kate**: למי שמעדיף ממשק גרפי

### קיצורי דרך שימושיים
#### Vim
```
גג - קפיצה לתחילת הקובץ
5גג - קפיצה לשורה 5
/ - חיפוש
% - קפיצה לסוגר תואם
```

#### Nano
```
Alt+U - ביטול פעולה
Alt+E - חזרה על פעולה
Alt+A - סימון טקסט
```

### הגדרות מומלצות

#### קובץ .vimrc בסיסי:
```vim
set number          " מספרי שורות
set autoindent      " הזחה אוטומטית
set showmatch       " הדגשת סוגריים תואמים
set incsearch       " חיפוש תוך כדי הקלדה
syntax on           " הדגשת תחביר
```

#### קובץ .nanorc בסיסי:
```bash
set linenumbers
set autoindent
set mouse
set tabsize 4
```

## פתרון בעיות נפוצות

### שחזור קבצים
- ב-Vim: חיפוש קבצי `.swp`
- ב-Nano: חיפוש קבצי `.save`

### בעיות נפוצות ב-Vim
1. תקוע במצב הכנסה:
   - לחץ על `Esc`

2. לא מצליח לצאת:
   - `:q!`

3. מקשי חצים לא עובדים:
   ```vim
   set nocompatible
   ```

### בעיות נפוצות ב-Nano
1. לא רואים את שורת הפקודות למטה:
   - הגדל את החלון

2. בעיות בעברית:
   - וודא שהמסוף מוגדר ל-UTF-8