# סביבת המשתמש בלינוקס - מדריך מקיף

## משתני סביבה

### מה הם משתני סביבה?
משתני סביבה הם ערכים שמשפיעים על התנהגות התוכניות במערכת.

### משתני סביבה חשובים
```bash
# הצגת כל משתני הסביבה
env

# משתנים חשובים:
echo $HOME          # תיקיית הבית
echo $PATH          # נתיב החיפוש לתוכניות
echo $USER          # שם המשתמש הנוכחי
echo $SHELL         # מעטפת ברירת המחדל
echo $LANG          # הגדרות שפה
echo $TERM          # סוג המסוף
echo $PWD           # תיקייה נוכחית
echo $EDITOR        # עורך טקסט ברירת מחדל
```

### עבודה עם משתני סביבה
```bash
# הגדרת משתנה זמני
export MY_VAR="ערך כלשהו"

# הצגת ערך משתנה
echo $MY_VAR

# מחיקת משתנה
unset MY_VAR

# הוספה לנתיב החיפוש
export PATH=$PATH:/תיקייה/חדשה
```

## קבצי הגדרות

### קבצי הגדרה מערכתיים
```bash
/etc/profile              # הגדרות מערכת כלליות
/etc/bash.bashrc          # הגדרות bash מערכתיות
/etc/environment          # משתני סביבה מערכתיים
```

### קבצי הגדרה אישיים
```bash
~/.bashrc                 # הגדרות אישיות ל-bash
~/.profile               # הגדרות אישיות כלליות
~/.bash_aliases          # הגדרות קיצורי דרך
~/.bash_history          # היסטוריית פקודות
~/.bash_logout           # פקודות להרצה בעת התנתקות
```

### דוגמה לקובץ .bashrc
```bash
# הגדרת צבעים
export CLICOLOR=1
export LSCOLORS=GxFxCxDxBxegedabagaced

# היסטוריה
HISTSIZE=1000
HISTFILESIZE=2000
HISTCONTROL=ignoreboth

# אליאסים שימושיים
alias ll='ls -la'
alias la='ls -A'
alias l='ls -CF'
alias cls='clear'

# פונקציות מותאמות אישית
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# הגדרת Prompt
PS1='\u@\h:\w\$ '

# הגדרת נתיב
export PATH=$PATH:$HOME/bin

# הגדרות לוקאליות
export LANG=he_IL.UTF-8
export LC_ALL=he_IL.UTF-8
```

## התאמה אישית

### התאמת Prompt
```bash
# רכיבים שימושיים ב-PS1:
\u - שם משתמש
\h - שם מחשב
\w - נתיב מלא
\W - תיקייה נוכחית
\t - שעה
\d - תאריך
\$ - # למשתמש root, $ למשתמש רגיל

# דוגמאות:
PS1='\u@\h:\w\$ '              # פורמט סטנדרטי
PS1='\[\033[32m\]\u@\h:\w\$ '  # עם צבע ירוק
PS1='\t \u \w\$ '              # עם שעה
```

### הגדרת אליאסים
```bash
# אליאסים שימושיים
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias search='apt search'
alias please='sudo'
alias ..='cd ..'
alias ...='cd ../..'
alias home='cd ~'
alias disk='df -h'
alias ports='netstat -tulanp'
```

### פונקציות מותאמות אישית
```bash
# פונקציה ליצירת תיקייה וכניסה אליה
function mkcd() {
    mkdir -p "$1" && cd "$1"
}

# פונקציה לחיפוש בהיסטוריה
function hg() {
    history | grep "$1"
}

# פונקציה לגיבוי קובץ
function backup() {
    cp "$1" "$1.bak"
}

# פונקציה להצגת מזג אוויר
function weather() {
    curl wttr.in/"$1"
}
```

## הגדרות מתקדמות

### התאמת מקשי קיצור
```bash
# הוספה ל-.inputrc
"\e[A": history-search-backward    # חץ למעלה
"\e[B": history-search-forward     # חץ למטה
"\e[1;5C": forward-word           # Ctrl+חץ ימינה
"\e[1;5D": backward-word          # Ctrl+חץ שמאלה
```

### הגדרת תצוגת היסטוריה
```bash
# הגדרות היסטוריה מתקדמות
HISTSIZE=10000                    # גודל היסטוריה בזיכרון
HISTFILESIZE=20000               # גודל קובץ היסטוריה
HISTCONTROL=ignoreboth           # התעלמות מכפילויות ורווחים
HISTIGNORE="ls:cd:exit:clear"    # פקודות להתעלמות
HISTTIMEFORMAT="%F %T "          # הוספת חותמת זמן
```

### הגדרת השלמה אוטומטית
```bash
# הוספה ל-.bashrc
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi

# הגדרות השלמה מותאמות אישית
complete -W "now tomorrow never" dothis
```

## פתרון בעיות

### בעיות נפוצות
1. שינויים ב-.bashrc לא משפיעים:
   ```bash
   source ~/.bashrc
   ```

2. משתני סביבה לא נטענים:
   - בדוק את ההרשאות של קבצי ההגדרה
   - וודא שהקבצים נקראים בסדר הנכון

3. בעיות עם לוקאליזציה:
   ```bash
   # בדיקת הגדרות נוכחיות
   locale
   
   # הגדרת לוקאל
   export LANG=he_IL.UTF-8
   ```

### טיפים לדיבוג
```bash
# הדפסת קבצים שנטענים
bash -x

# בדיקת תחביר של סקריפט
bash -n script.sh

# הדפסת פקודות בזמן הרצה
set -x
```

### גיבוי והחזרה
```bash
# גיבוי קבצי הגדרה
cp ~/.bashrc ~/.bashrc.bak
cp ~/.profile ~/.profile.bak

# שחזור מגיבוי
cp ~/.bashrc.bak ~/.bashrc
source ~/.bashrc
```
