# Макет
...
# Вёрстка
       BACK:
      ------------
      #* В терминале риадмишки(винда):
       1. cmd
       2. python3 --version Python 3.11.5
       3. -m venv env
       4. env\Scripts\activate
          *(python.exe -m pip install --upgrade pip)
       5. pip install requests
      # 1) бэкап
      import requests
      import sqlite3
      
      con = sqlite3.connect("backup.db")
      cur = con.cursor()
      cur.execute('''
          CREATE TABLE IF NOT EXISTS Tasks (
          id TEXT,
          name TEXT,
          description TEXT,
          due_date TEXT,
          is_complated INTEGER,
          created TEXT            
          )
      ''')
      
      
      data =requests.get("https://678bafd41a6b89b27a2b1cd4.mockapi.io/Task")
      for task in data.json():
          id =task["id"]
          name = task["name"]
          description=task["description"]
          due_date= task["due_date"]
          is_complated= task["is_complated"]
          created= task["created"]
          cur.execute('''INSERT INTO Tasks (id, name, description, due_date, is_complated, created) 
                      VALUES (?, ?, ?, ?, ?, ?)''', 
                      (id, name, description, due_date, is_complated, created ))
          print(f"Success backup")
      
      con.commit()
      con.close()
      -------------------

# MockAPI
![image](https://github.com/user-attachments/assets/5db423c0-623a-4b33-99f1-030a267bebd3)
