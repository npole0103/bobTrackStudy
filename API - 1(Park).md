# 클로바 API / 파파고 API

---

파파고 번역 API

``` py
import os
import sys
import urllib.request

client_id = '1Ag8DorrisfFnI_0IbJN'
client_pw = 'w9Ofr6h1vo'

encText = urllib.parse.quote("안녕하세요")

data = "source=ko&target=en&text=" + encText
url = "https://openapi.naver.com/v1/papago/n2mt"

request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id",client_id)
request.add_header("X-Naver-Client-Secret",client_pw)

response = urllib.request.urlopen(request, data=data.encode("utf-8"))
rescode = response.getcode()

if(rescode==200):
    response_body = response.read()
    print(response_body.decode('utf-8'))

else:
    print("Error Code", rescode)
```

---

클로바 인공지능 API

`pip install opencv-python` 필수

``` py
# 클로바 인공지능 얼굴인식 실습

# pip install opencv-python

import os
import sys
import urllib.request
import cv2
import requests

image = cv2.imread("image.jpg")
cv2.imshow("Hello", image)

# 클로바 인공지능 얼굴인식'
client_id = "GYMClxIoEUoD_1xQce5D"
client_secret = "aeuzNvnukd"

url = "https://openapi.naver.com/v1/vision/face"

filename = 'image.jpg'

image = cv2.imread(filename)
files = {'image' : open(filename, 'rb')}
headers = {'X-Naver-Client-Id': client_id, 'X-Naver-Client-Secret': client_secret}

response = requests.post(url, files=files, headers=headers)
rescode = response.status_code

if(rescode == 200):
    print(response.text)
else:
    print("Error Code:" + str(rescode))

data = response.json()
print(data)
if(data['info']['faceCount'] > 0) :
    for face in data['faces']:
        x1 = face['roi']['x']
        y1 = face['roi']['y']
        width = face['roi']['width']
        height = face['roi']['height']
        print("x={}, y={}, width={}, height={}".format(x1, y1, width, height), (0,0,255), 2)

        x1 = x1
        y1 = y1
        x2 = x1+width
        y2 = y1+height
        
        text = str(face['gender']['value']) + "(" + str(face['gender']['confidence']) + ")"
        text2 = "age : " + str(face['age']['value']) + "(" + str(face['age']['confidence']) + ")"
        text3 = str(face['emotion']['value']) + "(" + str(face['emotion']['confidence']) + ")"
        #color = BGR
        cv2.rectangle(image, (x1,y1), (x2, y2), (0,255,0), 2)
        cv2.putText(image, text, (x1, y1-20), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0,255,0), 2)
        cv2.putText(image, text2, (x1, y1 + 0), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0,255,0), 2)
        cv2.putText(image, text3, (x1, y1 + 20), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0,255,0), 2)


cv2.imshow("Myface", image)
cv2.waitKey(0)
```

---

