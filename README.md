# giftvoucher

# ลิ้งสำหรับ
http://103.141.68.26/api/free/ลิ้งอั่งเปา/เบอร์ผู้รับเงิน/

https://gift.truemoney.com/campaign/?v=ลิ้งอั่งเปา  <---- ลิ้งอั่งเปาคือลิ้งหลัง ?v= ตรงนี้นะครับ อย่าลืมเขียนตัด String กันด้วย


# Errors & Success

| code     | status  | message_en              | message                             |
| -------- | ------- | ----------------------- | ----------------------------------- |
| 100      | error   | VOUCHER_OUT_OF_STOCK    | ลิงค์ซองของขวัญถูกใช้งานแล้ว             |
| 101      | error   | VOUCHER_NOT_FOUND       | ลิงค์ซองของขวัญไม่ถูกต้อง                |
| 102      | error   | CANNOT_GET_OWN_VOUCHER  | ไม่สามารถใช้อั่งเปาของตัวเองได้            |
| 103      | error   | CANNOT_GET_MORE_ONE     | กรุณาเลือกให้รับซองได้เพียวคนเดียว         |
| 104      | error   | PLEASE_FILL_CORRECT     | ลิงค์ซองของขวัญหมดอายุ                 |
| 200      | success | SUCCESS_FOR_TOPUP       | ทำรายการเสร็จสิ้น                       |

# Response

```javascript
{
    "code": "200",                                //เช็ค code เอาไว้ดู status ตอบกลับ
    "status": "success",                          //status ตอบกลับ
    "data": {                                     //โชว์ Data ถ้าหาก status เป็น error Data จะเป็น Null
        "name": "xxxx",                           //ชื่อผู้เติม
        "tel": "08x-xxx-xxx",                      //เบอร์ที่รับเงิน
        "amount": xx                              //จำนวนที่ได้รับ
    },
    "message": "คุณได้เติมเงินมา : xx.00 บาท",       //ข้อความตอบกลับ ภาษาไทย
    "message_en": "You have top-up : xx.00 baht" //ข้อความตอบกลับ อังกฤษ
}
```

# โค้ดสำหรับดึงรายการภาษา PHP

```php
$url = "ลิ้งอั่งเปา";
$tel = "กรอกเบอร์ผู้รับ";
function giftvoucher($url, $tel){
        $curl = curl_init();
        curl_setopt_array($curl, array(
        CURLOPT_URL => 'http://103.141.68.26/api/free/'.$url.'/'.$tel.'/',
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'GET',
        ));
        $response = curl_exec($curl);
        curl_close($curl);
        return $response;
    }
```
