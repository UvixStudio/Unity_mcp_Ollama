# מדריך התקנה - Unity MCP עם Ollama

חיבור מודלי AI (דרך Ollama) ל-Unity Editor באמצעות Model Context Protocol.

## 🎯 מה זה עושה?

הפרוייקט הזה מאפשר לעוזרי AI לשלוט ב-Unity Editor ישירות דרך פקודות בשפה טבעית. אפשר לבקש מה-AI:
- ליצור ולשנות GameObjects
- לשנות חומרים וצבעים
- לנהל סצנות
- להוסיף קומפוננטות
- ועוד הרבה יותר!

## 📋 דרישות מקדימות

לפני שמתחילים, וודא שיש לך:

1. **Unity Editor** (מומלץ 2021.3 ומעלה)
2. **Python 3.12+** מותקן
3. **Conda** (Anaconda או Miniconda)
4. **Ollama** מותקן ורץ
5. **Git** לניהול גרסאות

## 🚀 מדריך התקנה

### שלב 1: התקנת Ollama

1. הורד והתקן את Ollama מ-[ollama.ai](https://ollama.ai)
2. משוך את מודל DeepSeek Coder:
   ```bash
   ollama pull deepseek-coder:latest
   ```
3. וודא ש-Ollama רץ:
   ```bash
   ollama list
   ```

### שלב 2: הגדרת סביבת Python

1. צור סביבת Conda חדשה:
   ```bash
   conda create -n unity-mcp python=3.12
   conda activate unity-mcp
   ```

2. התקן את חבילות Python הנדרשות:
   ```bash
   pip install httpx mcp fastapi uvicorn
   ```

### שלב 3: התקנת חבילת Unity MCP

1. פתח את פרוייקט Unity שלך
2. פתח את Package Manager (Window → Package Manager)
3. לחץ על כפתור **+** → Add package from git URL
4. הזן: `https://github.com/ZundamonnoVRChatkaisetu/unity-mcp-ollama.git`
5. המתן להתקנה להסתיים

### שלב 4: הגדרת שרת MCP

1. נווט ל: `Library/PackageCache/com.zundamonnovrchat.unity-mcp-ollama@[version]/Python/`
2. ערוך את `local_config.json`:
   ```json
   {
     "unity_host": "localhost",
     "unity_port": 6400,
     "mcp_port": 6500,
     "ollama_model": "deepseek-coder:latest",
     "ollama_host": "localhost",
     "ollama_port": 11434
   }
   ```

3. תקן את באג FastMCP ב-`server.py`:
   - פתח את `server.py`
   - מצא שורה עם `FastMCP("Unity MCP Server", description=...)`
   - הסר את פרמטר `description`
   - צריך להיראות כך: `mcp = FastMCP("Unity MCP Server")`

### שלב 5: הפעלת השרתים

1. **הפעל Unity Bridge** (ב-Unity Editor):
   - Unity Bridge אמור להתחיל אוטומטית כש-Unity נפתח
   - בדוק ב-Console את ההודעה "Unity Bridge listening on port 6400"

2. **הפעל Python MCP Server**:
   ```bash
   conda activate unity-mcp
   cd "Library/PackageCache/com.zundamonnovrchat.unity-mcp-ollama@[version]/Python/"
   python server.py
   ```

3. וודא חיבור ב-Unity Console - אמורות להופיע הודעות חיבור

## 🎮 דוגמאות שימוש

ברגע שהכל רץ, אפשר לשלוח פקודות ל-Unity דרך ממשק MCP.

### דוגמאות פקודות:
- "צור קוביה אדומה במיקום (0, 1, 0)"
- "שנה את הצבע של הכדור לכחול"
- "הוסף Rigidbody לשחקן"
- "צור 10 כדורים רנדומליים בסצנה"

## 🔧 פתרון בעיות

### Unity Bridge לא מתחיל
- בדוק ב-Unity Console אם יש שגיאות
- וודא שפורט 6400 לא בשימוש
- אתחל את Unity Editor

### שרת Python לא מתחבר
- וודא שסביבת Conda מופעלת
- בדוק אם Ollama רץ: `ollama list`
- וודא שפורטים 6400 ו-6500 זמינים
- בדוק הגדרות ב-`local_config.json`

### מודל Ollama לא נמצא
- משוך את המודל: `ollama pull deepseek-coder:latest`
- וודא עם: `ollama list`
- בדוק שם מודל ב-`local_config.json`

### שגיאת FastMCP
- הסר פרמטר `description` מאתחול `FastMCP()` ב-`server.py`
- זה באג ידוע בחבילה

## 📝 הערות חשובות

- מודלים של Ollama לא כלולים ברפוזיטורי בגלל הגודל שלהם
- צריך להוריד אותם בנפרד עם פקודת `ollama pull`
- Unity Bridge רץ על פורט 6400
- Python MCP Server רץ על פורט 6500
- Ollama רץ על פורט 11434

## 🙏 קרדיטים

- חבילת MCP מקורית: [unity-mcp-ollama](https://github.com/ZundamonnoVRChatkaisetu/unity-mcp-ollama)
- Ollama: [ollama.ai](https://ollama.ai)
- Model Context Protocol: [MCP](https://modelcontextprotocol.io)

---

**שים לב:** המודלים של Ollama לא נכללים ברפוזיטורי הזה בגלל הגודל שלהם. חובה להוריד אותם בנפרד.
