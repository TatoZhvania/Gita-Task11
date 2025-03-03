# 📌 **Task 1**

## **1. პროექტის სტრუქტურა შევქმენი**

პირველ რიგში, შევქმენი პროექტის დირექტორია და საჭირო ფაილები:

```bash
mkdir gita-final-n1
cd gita-final-n1
touch Dockerfile index.html server.py requirements.txt
```

---

## **2. `index.html` ფაილი დავამატე**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome</title>
</head>
<body>
    <h1>Hello, Tato Zhvania</h1>
</body>
</html>

```

---

## **3. Flask სერვერის კოდი დავწერე `server.py` ფაილში**

გამოვიყენე Flask-ის **send_file()** მეთოდი.

```python
from flask import Flask, send_file

app = Flask(__name__)

@app.route('/')
def home():
    return send_file('index.html')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)

```

---

## **4. `requirements.txt` ფაილში Flask ჩავწერე**

---

## **5. Dockerfile შევქმენი**

```docker
# გამოვიყენე პატარა ზომის Python image
FROM python:3.10-alpine

# სამუშაო დირექტორიის შექმნა
WORKDIR /app

# ყველა საჭირო ფაილის ერთდროულად კოპირება
COPY . /app/

# Flask-ის ინსტალაცია
RUN pip install --no-cache-dir -r requirements.txt

# პორტის გახსნა
EXPOSE 8000

# სერვერის გაშვების ბრძანება
CMD ["python", "server.py"]
```

აქ **ყველა ფაილი ერთიანად** დავაკოპირე `COPY . /app/`, რაც **Docker Image-ის აგებას უფრო სწრაფს ხდის**.

---

## **6. Docker Image ავაგე**

**Docker Image** ავაგე ჩემი დოკერჰაბის უსერნეიმით:

```bash
docker build -t tzhvania33/flask-webserver .
```

---

## **7. Docker Hub-ზე დავფუშე**

შემდეგ, **Docker Hub-ზე** ავტვირთე ჩემი იმიჯი: დალოგინებული ვიყავი უკვე და docker login ბრძანება არ დამჭირდა

```bash
docker push tzhvania33/flask-webserver
```

![image.png](attachment:6d8ad108-bd3d-49a3-b1ba-f7668debfe9b:image.png)

---

## **8. საბოლოო ტესტი**
