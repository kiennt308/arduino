# Floating Point Constants
**Floating Point Constants** trong Arduino là các giá trị số thực (có dấu chấm thập phân) được sử dụng trong chương trình để biểu thị số liệu với phần nguyên và phần thập phân. Arduino hỗ trợ các kiểu dữ liệu số thực như **float** và **double** (cả hai đều có kích thước 4 byte và độ chính xác tương tự nhau trên hầu hết các vi điều khiển AVR).

### Đặc điểm của Floating Point Constants trong Arduino:
1. **Biểu diễn số thực:**
   - Một số thực được viết với phần nguyên và phần thập phân, được phân cách bằng dấu chấm (`.`).
   - Ví dụ: `3.14`, `-0.001`, `123.456`.

2. **Ký hiệu khoa học (scientific notation):**
   - Floating point constants cũng có thể được biểu diễn bằng ký hiệu khoa học (exponential notation) với chữ `E` hoặc `e` để biểu thị mũ của 10.
   - Ví dụ: `2.5E3` tương đương với \(2.5 \times 10^3 = 2500\), và `1.2e-4` tương đương \(1.2 \times 10^{-4} = 0.00012\).

3. **Kiểu dữ liệu ngầm định:**
   - Các số thực được mặc định coi là kiểu **double** trên hầu hết các nền tảng, nhưng trên Arduino (các vi điều khiển AVR như ATmega328P), **double** và **float** có cùng độ chính xác (4 byte).
   - Bạn có thể gắn hậu tố `f` để chỉ định một hằng số là kiểu **float** rõ ràng:
     ```cpp
     float x = 3.14f;  // Kiểu float
     ```

4. **Hạn chế độ chính xác:**
   - Với 4 byte, các số thực kiểu float hoặc double trên Arduino có độ chính xác khoảng 6-7 chữ số thập phân. Điều này nghĩa là bạn không thể biểu diễn các số quá lớn hoặc quá nhỏ với độ chính xác cao.

### Sử dụng Floating Point Constants trong Arduino:
Floating point constants thường được dùng trong các tính toán số học yêu cầu độ chính xác cao hơn so với số nguyên, như trong các phép tính toán học phức tạp, đồ thị, hoặc cảm biến:

#### Ví dụ minh họa:
```cpp
void setup() {
  Serial.begin(9600);

  float pi = 3.14159;          // Hằng số kiểu float
  double scientific = 1.23e4;  // Hằng số dạng khoa học
  float radius = 5.0;
  float area = pi * radius * radius;  // Tính diện tích hình tròn

  Serial.println("Area of the circle:");
  Serial.println(area);
}

void loop() {
  // Không làm gì trong loop
}
```

### Lưu ý:
1. **Hiệu suất xử lý:** Các phép tính với floating point thường chậm hơn so với số nguyên do yêu cầu tính toán phức tạp hơn.
2. **Hạn chế bộ nhớ:** Floating point sử dụng nhiều bộ nhớ hơn so với số nguyên, vì vậy cần cân nhắc nếu bạn làm việc trên các vi điều khiển với tài nguyên hạn chế.
3. **Cần cẩn thận với sai số:** Do cách biểu diễn floating point trong máy tính, các phép tính có thể gây ra sai số nhỏ. 


# HIGH | LOW

Trong Arduino, **HIGH** và **LOW** là hai giá trị logic được sử dụng để biểu thị trạng thái **cao** và **thấp** của một chân (pin) trên vi điều khiển. Chúng được sử dụng chủ yếu trong việc điều khiển đầu ra và đọc trạng thái đầu vào của các chân số (digital pins).

### **HIGH** và **LOW** là gì?
1. **HIGH:**
   - Biểu thị mức logic **cao** (logical high).
   - Tương ứng với điện áp **5V** (hoặc **3.3V** trên các bo mạch Arduino chạy ở 3.3V như Arduino Due hoặc Nano 33 BLE).
   - Được biểu diễn bằng số nguyên **1**.

2. **LOW:**
   - Biểu thị mức logic **thấp** (logical low).
   - Tương ứng với điện áp **0V**.
   - Được biểu diễn bằng số nguyên **0**.

### Sử dụng **HIGH** và **LOW**
1. **Điều khiển đầu ra số (Digital Output):**
   Khi một chân được thiết lập là đầu ra (**OUTPUT**) bằng `pinMode(pin, OUTPUT);`, bạn có thể sử dụng `digitalWrite()` để đặt trạng thái của chân đó là **HIGH** hoặc **LOW**.

   Ví dụ:
   ```cpp
   void setup() {
     pinMode(13, OUTPUT);  // Đặt chân 13 là đầu ra
   }

   void loop() {
     digitalWrite(13, HIGH);  // Bật LED (chân 13 mức HIGH)
     delay(1000);             // Chờ 1 giây
     digitalWrite(13, LOW);   // Tắt LED (chân 13 mức LOW)
     delay(1000);             // Chờ 1 giây
   }
   ```

2. **Đọc trạng thái đầu vào số (Digital Input):**
   Khi một chân được thiết lập là đầu vào (**INPUT**) bằng `pinMode(pin, INPUT);`, bạn có thể sử dụng `digitalRead()` để kiểm tra xem chân đó đang ở trạng thái **HIGH** hay **LOW**.

   Ví dụ:
   ```cpp
   const int buttonPin = 2;  // Chân kết nối nút bấm
   const int ledPin = 13;    // Chân kết nối LED

   void setup() {
     pinMode(buttonPin, INPUT);  // Đặt chân 2 là đầu vào
     pinMode(ledPin, OUTPUT);    // Đặt chân 13 là đầu ra
   }

   void loop() {
     int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút bấm
     if (buttonState == HIGH) {  // Nếu nút bấm được nhấn (mức HIGH)
       digitalWrite(ledPin, HIGH);  // Bật LED
     } else {
       digitalWrite(ledPin, LOW);   // Tắt LED
     }
   }
   ```

### Lưu ý:
1. **Điện áp tham chiếu:**
   - Trạng thái **HIGH** và **LOW** phụ thuộc vào điện áp của bo mạch. Đối với các bo mạch Arduino chạy ở 5V, **HIGH** là 5V và **LOW** là 0V. Đối với bo mạch chạy ở 3.3V, **HIGH** là 3.3V.
   
2. **Pull-up/Pull-down Resistors:**
   - Nếu bạn sử dụng chân đầu vào số (**INPUT**) mà không có điện trở pull-up hoặc pull-down, trạng thái của chân có thể không ổn định (floating). Bạn có thể sử dụng điện trở ngoài hoặc kích hoạt điện trở pull-up nội bộ bằng cách sử dụng `pinMode(pin, INPUT_PULLUP);`.

3. **Thời gian trễ (Debouncing):**
   - Khi đọc trạng thái từ các nút bấm hoặc cảm biến, tín hiệu có thể bị nhiễu (bouncing). Cần sử dụng kỹ thuật **debouncing** để đảm bảo độ chính xác.

### Tóm tắt:
- **HIGH:** Tương ứng mức logic cao (5V hoặc 3.3V).
- **LOW:** Tương ứng mức logic thấp (0V).
- **Sử dụng:** Dùng để điều khiển hoặc kiểm tra trạng thái của các chân số trên Arduino.

# INPUT | INPUT_PULLUP | OUTPUT
Trong Arduino, các chế độ **INPUT**, **INPUT_PULLUP**, và **OUTPUT** được sử dụng để cấu hình chức năng của các chân (pins) của vi điều khiển. Các chế độ này được thiết lập bằng hàm `pinMode(pin, mode);`, trong đó `pin` là số chân và `mode` là một trong ba chế độ nói trên.

### 1. **INPUT**
- **Mô tả:**
  - Đặt chân thành đầu vào để đọc tín hiệu từ bên ngoài (nút bấm, cảm biến, công tắc, v.v.).
  - Ở chế độ này, chân có điện trở trở kháng cao (**high-impedance**), giúp giảm dòng điện tiêu thụ và hạn chế ảnh hưởng đến mạch bên ngoài.
  
- **Ứng dụng:**
  - Sử dụng để đọc trạng thái từ nút bấm, cảm biến hoặc các thiết bị đầu vào khác.

- **Ví dụ:**
  ```cpp
  const int buttonPin = 2;  // Chân kết nối nút bấm

  void setup() {
    pinMode(buttonPin, INPUT);  // Đặt chân 2 làm đầu vào
  }

  void loop() {
    int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút bấm
    if (buttonState == HIGH) {
      // Thực hiện hành động khi nút bấm được nhấn
    }
  }
  ```

- **Lưu ý:**
  - Nếu không có điện trở pull-up hoặc pull-down, chân có thể bị trôi (floating) và trả về trạng thái không ổn định.

---

### 2. **INPUT_PULLUP**
- **Mô tả:**
  - Đặt chân làm đầu vào với điện trở **pull-up nội bộ** được bật.
  - Khi bật chế độ này, chân được kết nối nội bộ với nguồn điện áp cao (5V hoặc 3.3V) thông qua một điện trở. Điều này giúp đảm bảo trạng thái mặc định của chân là **HIGH** nếu không có tín hiệu đầu vào.
  
- **Ứng dụng:**
  - Thường sử dụng với nút bấm hoặc cảm biến mà không cần thêm điện trở ngoài.

- **Ví dụ:**
  ```cpp
  const int buttonPin = 2;  // Chân kết nối nút bấm

  void setup() {
    pinMode(buttonPin, INPUT_PULLUP);  // Đặt chân 2 làm đầu vào với pull-up
  }

  void loop() {
    int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút bấm
    if (buttonState == LOW) {  // Nút bấm được nhấn (mức thấp)
      // Thực hiện hành động khi nút bấm được nhấn
    }
  }
  ```

- **Lưu ý:**
  - Trạng thái mặc định là **HIGH**. Khi nút bấm được nhấn và kết nối chân với **GND**, trạng thái sẽ chuyển thành **LOW**.

---

### 3. **OUTPUT**
- **Mô tả:**
  - Đặt chân làm đầu ra để điều khiển các thiết bị như LED, relay, motor, hoặc giao tiếp với các module khác.
  - Ở chế độ này, chân có thể xuất tín hiệu **HIGH** (5V hoặc 3.3V) hoặc **LOW** (0V).

- **Ứng dụng:**
  - Điều khiển thiết bị ngoại vi hoặc tạo tín hiệu logic.

- **Ví dụ:**
  ```cpp
  const int ledPin = 13;  // Chân kết nối LED

  void setup() {
    pinMode(ledPin, OUTPUT);  // Đặt chân 13 làm đầu ra
  }

  void loop() {
    digitalWrite(ledPin, HIGH);  // Bật LED
    delay(1000);                // Chờ 1 giây
    digitalWrite(ledPin, LOW);   // Tắt LED
    delay(1000);                // Chờ 1 giây
  }
  ```

- **Lưu ý:**
  - Khi chân được đặt ở mức **HIGH**, nó sẽ xuất điện áp cao (5V hoặc 3.3V).
  - Khi ở mức **LOW**, nó sẽ xuất điện áp thấp (0V).

---

### Tóm tắt so sánh:

| **Chế độ**       | **Mô tả**                                                                                   | **Ứng dụng**                            |
|-------------------|---------------------------------------------------------------------------------------------|-----------------------------------------|
| **INPUT**         | Đọc tín hiệu từ bên ngoài, chân có trở kháng cao.                                           | Đọc trạng thái nút bấm, cảm biến.       |
| **INPUT_PULLUP**  | Đọc tín hiệu từ bên ngoài, với điện trở pull-up nội bộ (mặc định trạng thái là HIGH).        | Đọc tín hiệu nút bấm, tiết kiệm điện trở. |
| **OUTPUT**        | Xuất tín hiệu điều khiển thiết bị, chân có thể đặt trạng thái HIGH hoặc LOW.                | Điều khiển LED, relay, motor.           |

# Integer Constants
### **Integer Constants trong Arduino**

**Integer Constants** trong Arduino là các giá trị số nguyên được định nghĩa trực tiếp trong mã chương trình. Chúng biểu diễn các con số không có dấu thập phân và có thể được sử dụng ở nhiều ngữ cảnh khác nhau như thiết lập biến, thực hiện tính toán, hoặc định nghĩa các hằng số.

---

### **1. Các kiểu Integer Constants**
Arduino hỗ trợ các kiểu số nguyên khác nhau, bao gồm:

#### **a. Decimal (Hệ thập phân)**
- Các số nguyên thông thường, được viết dưới dạng cơ số 10.
- Không có tiền tố đặc biệt.
- Ví dụ:
  ```cpp
  int myNumber = 100;  // Decimal constant
  ```

#### **b. Binary (Hệ nhị phân)**
- Các số nguyên được viết ở dạng nhị phân (0 và 1).
- Sử dụng tiền tố `0b` hoặc `0B`.
- Ví dụ:
  ```cpp
  int myBinary = 0b1010;  // Binary constant (tương ứng 10 trong thập phân)
  ```

#### **c. Octal (Hệ bát phân)**
- Các số nguyên được viết ở dạng cơ số 8 (0-7).
- Sử dụng tiền tố `0`.
- Ví dụ:
  ```cpp
  int myOctal = 012;  // Octal constant (tương ứng 10 trong thập phân)
  ```

#### **d. Hexadecimal (Hệ thập lục phân)**
- Các số nguyên được viết ở dạng cơ số 16 (0-9 và A-F).
- Sử dụng tiền tố `0x` hoặc `0X`.
- Ví dụ:
  ```cpp
  int myHex = 0x1A;  // Hexadecimal constant (tương ứng 26 trong thập phân)
  ```

---

### **2. Kích thước và kiểu của Integer Constants**
Arduino hỗ trợ các kiểu dữ liệu số nguyên với kích thước khác nhau, cụ thể:

| **Kiểu dữ liệu** | **Kích thước** | **Phạm vi giá trị**                         |
|------------------|----------------|---------------------------------------------|
| **byte**         | 8-bit          | 0 đến 255                                   |
| **int**          | 16-bit         | -32,768 đến 32,767                          |
| **unsigned int** | 16-bit         | 0 đến 65,535                                |
| **long**         | 32-bit         | -2,147,483,648 đến 2,147,483,647            |
| **unsigned long**| 32-bit         | 0 đến 4,294,967,295                         |

---

### **3. Biểu diễn ký tự cho Integer Constants**
Bạn có thể sử dụng các ký tự hậu tố để xác định kiểu của số nguyên:

- **`U`** hoặc **`u`**: Xác định là **unsigned**.
- **`L`** hoặc **`l`**: Xác định là **long**.
- **`UL`**, **`ul`**, **`LU`**, **`lu`**: Xác định là **unsigned long**.

#### **Ví dụ:**
```cpp
unsigned int myNumber = 100U;  // Xác định là unsigned int
long myBigNumber = 100000L;   // Xác định là long
unsigned long myVeryBig = 100000UL;  // Xác định là unsigned long
```

---

### **4. Sử dụng Integer Constants**
Integer Constants thường được sử dụng để:
1. **Định nghĩa hằng số:**
   ```cpp
   const int ledPin = 13;  // Số chân LED
   ```
2. **Thực hiện tính toán:**
   ```cpp
   int result = 5 + 10;  // Kết quả là 15
   ```
3. **Cấu hình thiết bị:**
   ```cpp
   analogWrite(ledPin, 255);  // Điều chỉnh độ sáng LED
   ```

---

### **5. Một số lưu ý khi dùng Integer Constants**
- **Tràn số:** Nếu bạn gán một giá trị vượt quá phạm vi của kiểu dữ liệu, kết quả có thể không như mong đợi.
  ```cpp
  int myNumber = 40000;  // Giá trị này vượt phạm vi của int (16-bit)
  ```

- **Cần đúng kiểu:** Nếu bạn sử dụng số nguyên lớn mà không xác định hậu tố kiểu, có thể xảy ra lỗi.
  ```cpp
  unsigned long bigNumber = 4294967296;  // Lỗi, vì số này vượt phạm vi của int.
  ```

---

### **Ví dụ thực tế:**
```cpp
const int ledPin = 13;  // Hằng số đại diện cho chân LED
const unsigned long delayTime = 1000UL;  // Thời gian trễ 1 giây

void setup() {
  pinMode(ledPin, OUTPUT);  // Thiết lập chân LED là đầu ra
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Bật LED
  delay(delayTime);           // Trì hoãn 1 giây
  digitalWrite(ledPin, LOW);   // Tắt LED
  delay(delayTime);           // Trì hoãn 1 giây
}
```

# LED_BUILTIN
### **LED_BUILTIN trong Arduino là gì?**

**`LED_BUILTIN`** là một hằng số được định nghĩa trong Arduino IDE để biểu thị chân kết nối với đèn LED tích hợp sẵn trên bo mạch Arduino. Hầu hết các bo mạch Arduino (như Arduino Uno, Mega, Nano, v.v.) đều có một đèn LED tích hợp mà bạn có thể sử dụng để thử nghiệm nhanh các chương trình hoặc chức năng mà không cần thêm phần cứng bên ngoài.

---

### **Chi tiết về LED_BUILTIN**
1. **Vị trí của LED_BUILTIN:**
   - Đèn LED này thường được kết nối với một chân GPIO cụ thể trên vi điều khiển, và giá trị của `LED_BUILTIN` sẽ tương ứng với số của chân đó.
   - Ví dụ:
     - Arduino Uno: `LED_BUILTIN` tương ứng với **chân 13**.
     - Arduino Nano: `LED_BUILTIN` tương ứng với **chân 13**.
     - Arduino Mega: `LED_BUILTIN` tương ứng với **chân 13**.
     - Arduino Leonardo: `LED_BUILTIN` tương ứng với **chân 13**.
     - ESP32/ESP8266: `LED_BUILTIN` có thể tương ứng với các chân khác (tùy thuộc vào module cụ thể).

2. **Mục đích của LED_BUILTIN:**
   - Dễ dàng kiểm tra mã nguồn mà không cần kết nối các thiết bị ngoại vi.
   - Hữu ích cho các ví dụ và bài học lập trình cơ bản (như ví dụ Blink mặc định của Arduino IDE).

3. **Cách sử dụng:**
   - `LED_BUILTIN` được sử dụng giống như bất kỳ chân GPIO nào khác.
   - Bạn có thể bật hoặc tắt đèn LED bằng cách sử dụng các hàm như `digitalWrite()`.

---

### **Ví dụ sử dụng LED_BUILTIN**

#### **Blink LED (Nhấp nháy đèn LED tích hợp):**
```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);  // Đặt LED_BUILTIN làm đầu ra
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // Bật LED
  delay(1000);                      // Chờ 1 giây
  digitalWrite(LED_BUILTIN, LOW);   // Tắt LED
  delay(1000);                      // Chờ 1 giây
}
```

#### **Điều khiển LED tích hợp bằng nút bấm:**
```cpp
const int buttonPin = 2;  // Chân kết nối nút bấm

void setup() {
  pinMode(buttonPin, INPUT);        // Đặt nút bấm làm đầu vào
  pinMode(LED_BUILTIN, OUTPUT);     // Đặt LED_BUILTIN làm đầu ra
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút bấm
  if (buttonState == HIGH) {
    digitalWrite(LED_BUILTIN, HIGH);         // Bật LED khi nút bấm được nhấn
  } else {
    digitalWrite(LED_BUILTIN, LOW);          // Tắt LED khi nút bấm không được nhấn
  }
}
```

---

### **Lưu ý khi sử dụng LED_BUILTIN**
1. **Khác biệt giữa các bo mạch:**
   - Một số bo mạch có thể không định nghĩa `LED_BUILTIN`, trong trường hợp này, bạn cần sử dụng số chân cụ thể mà LED được kết nối.
   - Trên ESP32 hoặc ESP8266, chân của LED tích hợp có thể khác với Arduino truyền thống.

2. **Khi sử dụng các bo mạch có nhiều LED:**
   - Một số bo mạch như ESP32 hoặc ESP8266 có nhiều LED tích hợp. Bạn cần kiểm tra tài liệu để biết chính xác chân kết nối.

3. **Độ sáng LED:**
   - Nếu đèn LED quá sáng hoặc không sáng, bạn có thể điều chỉnh bằng cách sử dụng điện trở thích hợp (trong trường hợp dùng LED ngoài).

---

### **Tóm tắt:**
- `LED_BUILTIN` là hằng số đại diện cho chân được kết nối với đèn LED tích hợp trên bo mạch Arduino.
- Hữu ích để kiểm tra nhanh các chương trình mà không cần thêm linh kiện phần cứng.
- Cách sử dụng tương tự như các chân GPIO thông thường.

# true | false
### **`true` | `false` trong Arduino là gì?**

Trong Arduino, **`true`** và **`false`** là hai giá trị boolean được sử dụng để biểu diễn các trạng thái logic:

- **`true`**: Đại diện cho trạng thái "đúng", tương đương với giá trị số **1**.
- **`false`**: Đại diện cho trạng thái "sai", tương đương với giá trị số **0**.

Chúng thuộc kiểu dữ liệu **`boolean`** và được sử dụng để kiểm soát luồng chương trình, đặc biệt trong các cấu trúc điều kiện và vòng lặp.

---

### **1. Định nghĩa kiểu boolean trong Arduino**
Arduino hỗ trợ kiểu dữ liệu **`boolean`** để làm việc với các giá trị logic:

```cpp
boolean myFlag = true;  // Biến boolean có giá trị true
```

- Giá trị **boolean** chỉ có thể là **`true`** hoặc **`false`**.
- **`true`** được ánh xạ thành **1** và **`false`** được ánh xạ thành **0** khi sử dụng trong các phép toán hoặc biểu thức.

---

### **2. Sử dụng `true` và `false` trong Arduino**

#### **a. Cấu trúc điều kiện**
Bạn có thể sử dụng **`true`** và **`false`** trong các câu lệnh điều kiện như `if` hoặc `while`:

```cpp
boolean isOn = false;

void setup() {
  Serial.begin(9600);
}

void loop() {
  if (isOn) {
    Serial.println("Đèn đang bật!");
  } else {
    Serial.println("Đèn đang tắt!");
  }
  delay(1000);
  isOn = !isOn;  // Đổi trạng thái giữa true và false
}
```

#### **b. Vòng lặp**
Các vòng lặp `while` có thể sử dụng **`true`** để tạo vòng lặp vô hạn hoặc dựa trên điều kiện logic:

```cpp
void loop() {
  while (true) {
    Serial.println("Vòng lặp vô hạn!");
    delay(1000);
  }
}
```

#### **c. Biểu thức logic**
Kết hợp **`true`** và **`false`** trong các biểu thức logic:

```cpp
boolean isButtonPressed = false;

void loop() {
  if (!isButtonPressed) {
    Serial.println("Nút chưa được nhấn.");
  } else {
    Serial.println("Nút đã được nhấn.");
  }
}
```

---

### **3. Cách Arduino xử lý `true` và `false`**
- Arduino coi **bất kỳ giá trị khác 0** là **`true`**.
- Chỉ giá trị **0** mới được coi là **`false`**.

#### **Ví dụ:**
```cpp
int myValue = 10;

if (myValue) {
  Serial.println("Giá trị khác 0 => true");
} else {
  Serial.println("Giá trị là 0 => false");
}
```

---

### **4. Các trường hợp sử dụng phổ biến**
- **Điều kiện bật/tắt thiết bị:**
  ```cpp
  boolean ledState = false;

  void loop() {
    if (ledState) {
      digitalWrite(LED_BUILTIN, HIGH);  // Bật LED
    } else {
      digitalWrite(LED_BUILTIN, LOW);   // Tắt LED
    }
    delay(1000);
    ledState = !ledState;  // Đổi trạng thái
  }
  ```

- **Theo dõi trạng thái cảm biến:**
  ```cpp
  boolean isSensorActive = digitalRead(sensorPin);

  if (isSensorActive == true) {
    Serial.println("Cảm biến đang hoạt động.");
  } else {
    Serial.println("Cảm biến không hoạt động.");
  }
  ```

---

### **5. Một số lưu ý khi sử dụng**
- **Kiểu dữ liệu boolean**:
  - Arduino hỗ trợ kiểu `boolean`, nhưng cũng có thể sử dụng `int` với giá trị **0** và **1** nếu cần tương thích với các thư viện cũ.
  - Ví dụ:
    ```cpp
    int flag = 1;  // Tương tự true
    if (flag) {
      Serial.println("Đúng");
    }
    ```

- **Tiết kiệm bộ nhớ**:
  - Mỗi biến `boolean` chiếm **1 byte** bộ nhớ, trong khi nó chỉ cần **1 bit** để lưu trữ trạng thái. Khi cần tối ưu hóa, hãy nhóm các trạng thái boolean vào một biến số nguyên.

---

### **Tóm tắt:**
- **`true`** và **`false`** là hai giá trị logic cơ bản trong Arduino.
- Chúng được sử dụng để kiểm soát luồng chương trình, xử lý các trạng thái bật/tắt, hoặc kết hợp trong các biểu thức logic.
- Mọi giá trị khác **0** đều được coi là **`true`**, còn **0** được coi là **`false`**.


# Data Types
Dưới đây là mô tả chi tiết các kiểu dữ liệu mà bạn đã liệt kê, bao gồm cả ví dụ và giải thích về cách sử dụng chúng trong Arduino:

---

### **1. array (Mảng)**
- **Mô tả:**
  - Mảng là một cấu trúc dữ liệu có thể lưu trữ nhiều giá trị cùng loại.
  - Các phần tử trong mảng có thể được truy cập thông qua chỉ mục (index).
- **Ví dụ:**
  ```cpp
  int numbers[5] = {1, 2, 3, 4, 5};

  void setup() {
    Serial.begin(9600);
    for (int i = 0; i < 5; i++) {
      Serial.println(numbers[i]);
    }
  }
  ```

---

### **2. bool**
- **Mô tả:**
  - Lưu trữ giá trị logic **`true`** hoặc **`false`**.
  - Là kiểu dữ liệu có kích thước 1 byte trên một số vi điều khiển.
- **Ví dụ:**
  ```cpp
  bool isOn = true;

  void loop() {
    if (isOn) {
      Serial.println("Đang bật!");
    } else {
      Serial.println("Đang tắt!");
    }
    delay(1000);
  }
  ```

---

### **3. boolean**
- **Mô tả:**
  - Tương tự như `bool`, lưu trữ giá trị **`true`** hoặc **`false`**.
  - **`boolean`** là một từ khóa kiểu dữ liệu đặc biệt trong Arduino (không có sự khác biệt lớn giữa `bool` và `boolean` trong Arduino).
- **Ví dụ:**
  ```cpp
  boolean lightOn = false;

  void loop() {
    if (lightOn) {
      digitalWrite(LED_BUILTIN, HIGH);
    } else {
      digitalWrite(LED_BUILTIN, LOW);
    }
    delay(1000);
  }
  ```

---

### **4. byte**
- **Mô tả:**
  - Lưu trữ số nguyên không dấu từ **0 đến 255**.
  - Chiếm 1 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  byte counter = 0;

  void loop() {
    Serial.println(counter);
    counter++;
    delay(1000);
  }
  ```

---

### **5. char**
- **Mô tả:**
  - Lưu trữ một ký tự ASCII hoặc một số nguyên có dấu trong phạm vi **-128 đến 127**.
  - Chiếm 1 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  char c = 'A';

  void loop() {
    Serial.println(c);
    delay(1000);
  }
  ```

---

### **6. double**
- **Mô tả:**
  - Lưu trữ số thực, có dấu với độ chính xác cao hơn **`float`**. Tuy nhiên, trên một số vi điều khiển, `double` và `float` có cùng độ chính xác.
  - Chiếm 4 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  double pi = 3.14159265359;

  void loop() {
    Serial.println(pi, 10);
    delay(1000);
  }
  ```

---

### **7. float**
- **Mô tả:**
  - Lưu trữ số thực, có dấu.
  - Chiếm 4 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  float temp = 25.5;

  void loop() {
    Serial.println(temp);
    delay(1000);
  }
  ```

---

### **8. int**
- **Mô tả:**
  - Lưu trữ số nguyên có dấu từ **-32,768 đến 32,767** (16-bit).
  - Chiếm 2 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  int counter = 100;

  void loop() {
    Serial.println(counter);
    counter++;
    delay(1000);
  }
  ```

---

### **9. long**
- **Mô tả:**
  - Lưu trữ số nguyên có dấu từ **-2,147,483,648 đến 2,147,483,647** (32-bit).
  - Chiếm 4 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  long largeNumber = 1000000000;

  void loop() {
    Serial.println(largeNumber);
    delay(1000);
  }
  ```

---

### **10. short**
- **Mô tả:**
  - Lưu trữ số nguyên có dấu từ **-32,768 đến 32,767** (16-bit).
  - Chiếm 2 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  short smallNumber = 200;

  void loop() {
    Serial.println(smallNumber);
    delay(1000);
  }
  ```

---

### **11. size_t**
- **Mô tả:**
  - Là kiểu dữ liệu không dấu, được sử dụng để chỉ số lượng hoặc kích thước, thường được sử dụng trong các chỉ số mảng hoặc số lượng phần tử.
  - Kích thước của `size_t` phụ thuộc vào kiến trúc của vi điều khiển (thường là 2 byte trên vi điều khiển 8-bit và 4 byte trên vi điều khiển 32-bit).
- **Ví dụ:**
  ```cpp
  size_t arraySize = 10;
  int arr[arraySize] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

  void loop() {
    for (size_t i = 0; i < arraySize; i++) {
      Serial.println(arr[i]);
    }
    delay(1000);
  }
  ```

---

### **12. string**
- **Mô tả:**
  - Là kiểu chuỗi ký tự đơn giản (không phải là đối tượng `String()` trong Arduino).
  - Thường được sử dụng trong C++ chuẩn, nhưng có thể sử dụng trong Arduino thông qua thư viện `String.h`.
- **Ví dụ:**
  ```cpp
  string message = "Hello, World!";

  void loop() {
    Serial.println(message.c_str());  // Chuyển đổi `string` thành `char[]` để in ra
    delay(1000);
  }
  ```

---

### **13. String()**
- **Mô tả:**
  - Là một lớp đối tượng trong Arduino để làm việc với chuỗi ký tự.
  - Khác với kiểu **`char[]`**, `String` cho phép sử dụng các phương thức thao tác với chuỗi ký tự một cách dễ dàng.
- **Ví dụ:**
  ```cpp
  String message = "Hello";

  void loop() {
    message += " Arduino!";  // Nối chuỗi
    Serial.println(message);
    delay(1000);
  }
  ```

---

### **14. unsigned char**
- **Mô tả:**
  - Lưu trữ số nguyên không dấu từ **0 đến 255**.
  - Chiếm 1 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  unsigned char value = 200;

  void loop() {
    Serial.println(value);
    delay(1000);
  }
  ```

---

### **15. unsigned int**
- **Mô tả:**
  - Lưu trữ số nguyên không dấu từ **0 đến 65,535**.
  - Chiếm 2 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  unsigned int count = 60000;

  void loop() {
    Serial.println(count);
    delay(1000);
  }
  ```

---

### **16. unsigned long**
- **Mô tả:**
  - Lưu trữ số nguyên không dấu từ **0 đến 4,294,967,295**.
  - Chiếm 4 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  unsigned long timestamp = millis();

  void loop() {
    Serial.println(timestamp);
    delay(1000);
  }
  ```

---

### **17. void**
- **Mô tả:**
  - Dùng để chỉ các hàm không trả về giá trị.
- **Ví dụ:**
  ```cpp
  void setup() {
    Serial.begin(9600);
  }

  void loop() {
    Serial.println("Đây là hàm không trả về giá trị");
    delay(1000);
  }
  ```

---

### **18. word**
- **Mô tả:**
  - Là kiểu dữ liệu số nguyên không dấu tương tự như **`unsigned int`**, nhưng giá trị của nó nằm trong phạm vi **0 đến 65,535**.
  - Chiếm 2 byte bộ nhớ.
- **Ví dụ:**
  ```cpp
  word temperature = 1000;

  void loop() {
    Serial.println(temperature);
    delay(1000);
  }
  ```

---

Dưới đây là bảng tóm tắt các kiểu dữ liệu trong Arduino mà bạn yêu cầu:

| **Kiểu Dữ Liệu**   | **Mô Tả**                                                | **Phạm Vi Giá Trị**                               | **Kích Thước Bộ Nhớ** |
|--------------------|----------------------------------------------------------|-------------------------------------------------|-----------------------|
| **array**          | Cấu trúc dữ liệu chứa nhiều giá trị cùng loại.           | Tùy thuộc vào số phần tử.                       | Tùy thuộc vào kích thước mảng |
| **bool**           | Lưu trữ giá trị logic `true` hoặc `false`.                | `true` hoặc `false`                              | 1 byte                |
| **boolean**        | Tương tự `bool`, lưu trữ giá trị logic `true` hoặc `false`. | `true` hoặc `false`                              | 1 byte                |
| **byte**           | Số nguyên không dấu từ 0 đến 255.                        | 0 đến 255                                         | 1 byte                |
| **char**           | Lưu trữ ký tự ASCII hoặc số nguyên có dấu.                | -128 đến 127                                      | 1 byte                |
| **double**         | Số thực với độ chính xác cao hơn `float`.                | Tùy thuộc vào vi điều khiển (thường giống `float`) | 4 byte                |
| **float**          | Số thực có dấu, độ chính xác thấp hơn `double`.           | Tùy thuộc vào vi điều khiển                      | 4 byte                |
| **int**            | Số nguyên có dấu từ -32,768 đến 32,767.                  | -32,768 đến 32,767                               | 2 byte                |
| **long**           | Số nguyên có dấu từ -2,147,483,648 đến 2,147,483,647.    | -2,147,483,648 đến 2,147,483,647                 | 4 byte                |
| **short**          | Số nguyên có dấu từ -32,768 đến 32,767.                  | -32,768 đến 32,767                               | 2 byte                |
| **size_t**         | Dùng để chỉ số lượng hoặc kích thước.                    | Tùy thuộc vào kiến trúc vi điều khiển            | 2 byte (8-bit) hoặc 4 byte (32-bit) |
| **string**         | Chuỗi ký tự trong C++ chuẩn (không phải `String()` Arduino). | Tùy thuộc vào chuỗi ký tự                        | Tùy thuộc vào chiều dài chuỗi |
| **String()**       | Lớp đối tượng dùng cho chuỗi ký tự trong Arduino.           | Tùy thuộc vào chuỗi ký tự                        | Tùy thuộc vào chuỗi ký tự |
| **unsigned char**  | Số nguyên không dấu từ 0 đến 255.                        | 0 đến 255                                         | 1 byte                |
| **unsigned int**   | Số nguyên không dấu từ 0 đến 65,535.                     | 0 đến 65,535                                      | 2 byte                |
| **unsigned long**  | Số nguyên không dấu từ 0 đến 4,294,967,295.              | 0 đến 4,294,967,295                              | 4 byte                |
| **void**           | Dùng cho các hàm không trả về giá trị.                    | Không có giá trị trả về                           | -                     |
| **word**           | Số nguyên không dấu từ 0 đến 65,535 (tương tự `unsigned int`). | 0 đến 65,535                                      | 2 byte                |



# Variable Scope & Qualifiers
Dưới đây là mô tả, giải thích và ví dụ về các **Variable Scope & Qualifiers** trong Arduino:

### 1. **`const` (Constant)**

- **Mô Tả**: Từ khóa `const` được sử dụng để khai báo một biến có giá trị không thay đổi trong suốt quá trình chạy của chương trình. Biến này có thể là `int`, `float`, hoặc bất kỳ kiểu dữ liệu nào.
- **Giải Thích**: Khi khai báo một biến với `const`, bạn không thể thay đổi giá trị của nó sau khi đã gán giá trị ban đầu. Điều này giúp tránh việc thay đổi giá trị của biến một cách vô tình, giữ cho chương trình ổn định hơn.
- **Ví Dụ**:
  ```cpp
  const int ledPin = 13;  // Đặt giá trị cho biến ledPin là 13, không thể thay đổi
  void setup() {
    pinMode(ledPin, OUTPUT); // Sử dụng ledPin như một chân đầu ra
  }

  void loop() {
    digitalWrite(ledPin, HIGH);  // Bật đèn LED
    delay(1000);
    digitalWrite(ledPin, LOW);   // Tắt đèn LED
    delay(1000);
  }
  ```
  Trong ví dụ trên, `ledPin` được khai báo là `const`, vì vậy bạn không thể thay đổi giá trị của nó trong suốt chương trình.

### 2. **Scope (Phạm Vi Biến)**

- **Mô Tả**: `Scope` của một biến xác định khu vực trong chương trình mà biến đó có thể được truy cập và sử dụng. Biến có thể có phạm vi toàn cục (global) hoặc phạm vi cục bộ (local).
  - **Global Scope**: Biến khai báo bên ngoài tất cả các hàm có phạm vi sử dụng toàn chương trình.
  - **Local Scope**: Biến khai báo trong một hàm chỉ có thể được sử dụng trong hàm đó.
  
- **Giải Thích**:
  - **Biến toàn cục** được khai báo bên ngoài bất kỳ hàm nào và có thể được truy cập từ bất kỳ hàm nào trong chương trình.
  - **Biến cục bộ** được khai báo trong một hàm và chỉ có thể được sử dụng trong hàm đó.
  
- **Ví Dụ**:
  ```cpp
  int globalVar = 10;  // Biến toàn cục
  
  void setup() {
    Serial.begin(9600);
    Serial.println(globalVar);  // Có thể truy cập globalVar
  }

  void loop() {
    int localVar = 5;  // Biến cục bộ
    Serial.println(localVar);  // Chỉ có thể sử dụng localVar trong hàm loop
    delay(1000);
  }
  ```
  Trong ví dụ trên:
  - `globalVar` có thể được truy cập từ cả `setup()` và `loop()`.
  - `localVar` chỉ có thể được sử dụng trong hàm `loop()`.

### 3. **`static`**

- **Mô Tả**: Từ khóa `static` được sử dụng để khai báo một biến có **phạm vi cục bộ**, nhưng **giữ lại giá trị của nó giữa các lần gọi hàm**.
- **Giải Thích**: Biến `static` chỉ được khởi tạo một lần và sẽ không bị xóa khi hàm kết thúc. Nó giữ lại giá trị của mình giữa các lần gọi hàm. Đây là một cách để theo dõi hoặc lưu trữ thông tin trong nhiều lần gọi mà không cần sử dụng biến toàn cục.
  
- **Ví Dụ**:
  ```cpp
  void countUp() {
    static int counter = 0;  // Biến static
    counter++;
    Serial.println(counter);
  }

  void setup() {
    Serial.begin(9600);
  }

  void loop() {
    countUp();  // Gọi hàm countUp liên tục, giá trị của counter sẽ được lưu lại
    delay(1000);
  }
  ```
  Trong ví dụ trên, biến `counter` sẽ không bị khởi tạo lại mỗi lần gọi hàm `countUp()`, mà sẽ giữ giá trị từ lần gọi trước đó. Kết quả in ra sẽ là một chuỗi các giá trị tăng dần.

### 4. **`volatile`**

- **Mô Tả**: Từ khóa `volatile` được sử dụng để khai báo một biến có thể thay đổi bất cứ lúc nào, ngoài sự kiểm soát của chương trình (ví dụ, khi có ngắt, phần cứng thay đổi giá trị biến, hoặc thay đổi bởi một quá trình khác).
- **Giải Thích**: Khi khai báo một biến là `volatile`, nó thông báo cho trình biên dịch rằng giá trị của biến có thể thay đổi bất kỳ lúc nào, vì vậy trình biên dịch sẽ không tối ưu hóa mã liên quan đến biến đó.
- **Ví Dụ**:
  ```cpp
  volatile int interruptFlag = 0;  // Biến volatile
  
  void setup() {
    Serial.begin(9600);
    attachInterrupt(digitalPinToInterrupt(2), interruptHandler, FALLING);  // Ngắt trên chân 2
  }

  void loop() {
    if (interruptFlag == 1) {
      Serial.println("Interrupt occurred!");
      interruptFlag = 0;  // Reset flag sau khi xử lý ngắt
    }
  }

  void interruptHandler() {
    interruptFlag = 1;  // Cập nhật giá trị khi có ngắt
  }
  ```
  Trong ví dụ trên, `interruptFlag` được khai báo là `volatile` vì nó có thể thay đổi bất ngờ khi có ngắt. Nếu không có từ khóa `volatile`, trình biên dịch có thể tối ưu hóa mã và không phát hiện sự thay đổi của biến này trong hàm `loop()`.

---

### Tổng kết:

| **Từ khóa**   | **Mô Tả**                                                                                              | **Ví Dụ**                                                           |
|---------------|------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|
| **`const`**   | Được sử dụng để khai báo một biến có giá trị không thay đổi trong suốt chương trình.                  | `const int ledPin = 13;`                                           |
| **`scope`**   | Quy định phạm vi mà biến có thể truy cập: toàn cục (global) hoặc cục bộ (local).                      | `int globalVar;` (global) vs `int localVar;` (local)                |
| **`static`**  | Biến có phạm vi cục bộ nhưng giữ lại giá trị giữa các lần gọi hàm.                                    | `static int counter = 0;`                                           |
| **`volatile`**| Biến có thể thay đổi ngoài sự kiểm soát của chương trình (ví dụ: ngắt, phần cứng).                   | `volatile int interruptFlag;`                                       |



# Conversion
### Conversion trong Arduino

Trong Arduino, **Conversion** là quá trình chuyển đổi giữa các kiểu dữ liệu để phù hợp với yêu cầu xử lý của chương trình. Dưới đây là mô tả, giải thích, và ví dụ cụ thể cho các hàm và biểu thức chuyển đổi trong Arduino.

---

### 1. **`byte()`**

- **Mô Tả**: Chuyển đổi một giá trị sang kiểu dữ liệu `byte` (8-bit).
- **Giải Thích**: Chỉ giữ lại 8-bit thấp nhất của giá trị đầu vào, bỏ qua các bit cao hơn nếu có.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = 300;
    byte y = byte(x);  // Chuyển đổi x thành kiểu byte (giá trị chỉ là 300 % 256)
    Serial.println(y);  // Kết quả: 44 (300 - 256 = 44)
  }

  void loop() {}
  ```

---

### 2. **`char()`**

- **Mô Tả**: Chuyển đổi một giá trị sang kiểu ký tự ASCII (`char`).
- **Giải Thích**: Dùng giá trị đầu vào để ánh xạ tới mã ASCII tương ứng.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = 65;  // Mã ASCII của 'A'
    char y = char(x);  // Chuyển đổi sang ký tự
    Serial.println(y);  // Kết quả: A
  }

  void loop() {}
  ```

---

### 3. **`float()`**

- **Mô Tả**: Chuyển đổi một giá trị số nguyên sang kiểu số thực (`float`).
- **Giải Thích**: Dùng để thực hiện các phép toán yêu cầu độ chính xác cao hơn, như số thập phân.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = 10;
    float y = float(x) / 3;  // Chuyển đổi x thành float và chia
    Serial.println(y);  // Kết quả: 3.33 (hoặc tương tự)
  }

  void loop() {}
  ```

---

### 4. **`int()`**

- **Mô Tả**: Chuyển đổi một giá trị số thực hoặc số kiểu khác sang số nguyên (`int`).
- **Giải Thích**: Loại bỏ phần thập phân nếu có và giữ lại phần nguyên.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    float x = 10.75;
    int y = int(x);  // Chuyển đổi sang số nguyên
    Serial.println(y);  // Kết quả: 10
  }

  void loop() {}
  ```

---

### 5. **`long()`**

- **Mô Tả**: Chuyển đổi giá trị sang kiểu số nguyên dài (`long`) 32-bit.
- **Giải Thích**: Dùng cho các giá trị lớn hơn phạm vi của kiểu `int` (16-bit trên Arduino).
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = 1000;
    long y = long(x) * 1000;  // Nhân giá trị x và ép kiểu sang long
    Serial.println(y);  // Kết quả: 1000000
  }

  void loop() {}
  ```

---

### 6. **`(unsigned int)`**

- **Mô Tả**: Chuyển đổi giá trị sang kiểu số nguyên không dấu (`unsigned int`) 16-bit.
- **Giải Thích**: Dùng để xử lý các giá trị không âm, tăng phạm vi từ 0 đến 65535.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = -100;  // Giá trị âm
    unsigned int y = (unsigned int)x;  // Chuyển đổi sang unsigned int
    Serial.println(y);  // Kết quả: 65436 (do 65536 - 100)
  }

  void loop() {}
  ```

---

### 7. **`(unsigned long)`**

- **Mô Tả**: Chuyển đổi giá trị sang kiểu số nguyên không dấu dài (`unsigned long`) 32-bit.
- **Giải Thích**: Dùng để xử lý các giá trị lớn hơn, với phạm vi từ 0 đến 4,294,967,295.
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    int x = -1;
    unsigned long y = (unsigned long)x;  // Chuyển đổi sang unsigned long
    Serial.println(y);  // Kết quả: 4294967295 (do underflow)
  }

  void loop() {}
  ```

---

### 8. **`word()`**

- **Mô Tả**: Kết hợp hai byte thành một giá trị kiểu `word` (16-bit).
- **Giải Thích**: Hữu ích khi làm việc với dữ liệu 16-bit (như giá trị từ cảm biến).
- **Ví Dụ**:
  ```cpp
  void setup() {
    Serial.begin(9600);
    byte highByte = 0x12;  // Giá trị byte cao
    byte lowByte = 0x34;   // Giá trị byte thấp
    word combined = word(highByte, lowByte);  // Kết hợp hai byte
    Serial.println(combined, HEX);  // Kết quả: 1234
  }

  void loop() {}
  ```

---

### Tóm Tắt:

| **Hàm/Chuyển đổi**       | **Mô Tả**                                                                                     | **Ví Dụ Kết Quả**                                    |
|---------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------|
| **`byte()`**             | Chuyển sang kiểu byte (8-bit).                                                              | `byte(300)` → `44`                                 |
| **`char()`**             | Chuyển sang ký tự ASCII.                                                                    | `char(65)` → `'A'`                                 |
| **`float()`**            | Chuyển sang số thực.                                                                        | `float(10) / 3` → `3.33`                          |
| **`int()`**              | Chuyển sang số nguyên, loại bỏ phần thập phân.                                              | `int(10.75)` → `10`                                |
| **`long()`**             | Chuyển sang số nguyên dài (32-bit).                                                         | `long(1000) * 1000` → `1000000`                   |
| **`(unsigned int)`**     | Chuyển sang số nguyên không dấu (16-bit).                                                   | `(unsigned int)(-100)` → `65436`                  |
| **`(unsigned long)`**    | Chuyển sang số nguyên dài không dấu (32-bit).                                               | `(unsigned long)(-1)` → `4294967295`              |
| **`word()`**             | Kết hợp hai byte thành một giá trị kiểu `word` (16-bit).                                    | `word(0x12, 0x34)` → `1234` (hexadecimal)         |



# Utilities

### **Utilities trong Arduino**

Các tiện ích (**Utilities**) trong Arduino như `PROGMEM` và `sizeof()` cung cấp công cụ để tối ưu hóa và xử lý dữ liệu hiệu quả hơn trong chương trình của bạn. Dưới đây là mô tả, giải thích, và ví dụ chi tiết.

---

### **1. `PROGMEM`**

#### **Mô tả:**
- `PROGMEM` là từ khóa dùng để lưu trữ dữ liệu hằng số trong bộ nhớ Flash (Program Memory) thay vì bộ nhớ SRAM.
- Arduino có dung lượng SRAM giới hạn, nên sử dụng `PROGMEM` giúp tiết kiệm bộ nhớ động.

#### **Giải thích:**
- Khi bạn khai báo một mảng hoặc hằng số lớn, mặc định chúng được lưu trữ trong SRAM. Với `PROGMEM`, dữ liệu sẽ được giữ trong Flash và chỉ truy xuất khi cần.

#### **Ví dụ:**
```cpp
#include <avr/pgmspace.h>  // Thư viện hỗ trợ PROGMEM

const char text[] PROGMEM = "Hello, PROGMEM!";  // Lưu chuỗi vào Flash

void setup() {
  Serial.begin(9600);

  // Đọc dữ liệu từ Flash từng ký tự
  for (int i = 0; i < strlen_P(text); i++) {
    char c = pgm_read_byte(&text[i]);  // Truy xuất từng byte
    Serial.print(c);
  }
}

void loop() {}
```

#### **Kết quả:** 
- Chuỗi `"Hello, PROGMEM!"` được in ra màn hình Serial Monitor, nhưng không tiêu tốn bộ nhớ SRAM.

---

### **2. `sizeof()`**

#### **Mô tả:**
- `sizeof()` là một toán tử trong C++ được sử dụng để trả về kích thước (số byte) của một biến, mảng, hoặc kiểu dữ liệu.

#### **Giải thích:**
- Dùng để kiểm tra kích thước của dữ liệu trong bộ nhớ.
- Hữu ích khi làm việc với mảng để tránh vượt quá kích thước cho phép.

#### **Ví dụ 1: Kiểm tra kích thước mảng**
```cpp
void setup() {
  Serial.begin(9600);

  int myArray[] = {10, 20, 30, 40, 50};
  int arraySize = sizeof(myArray) / sizeof(myArray[0]);  // Kích thước mảng

  Serial.print("Số phần tử trong mảng: ");
  Serial.println(arraySize);
}

void loop() {}
```

#### **Kết quả:** 
- In ra: `Số phần tử trong mảng: 5`.

#### **Ví dụ 2: Kiểm tra kích thước các kiểu dữ liệu**
```cpp
void setup() {
  Serial.begin(9600);

  Serial.print("Kích thước của int: ");
  Serial.println(sizeof(int));  // Kết quả: 2 (trên Arduino UNO)

  Serial.print("Kích thước của float: ");
  Serial.println(sizeof(float));  // Kết quả: 4

  Serial.print("Kích thước của char: ");
  Serial.println(sizeof(char));  // Kết quả: 1
}

void loop() {}
```

---

### **Tóm tắt bảng so sánh**

| **Utility**     | **Mô tả**                                                                                        | **Ứng dụng**                                                                                      | **Ví dụ Kết quả**                       |
|------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------|
| **`PROGMEM`**   | Lưu dữ liệu hằng số vào Flash thay vì SRAM để tiết kiệm bộ nhớ.                                   | Dùng khi làm việc với mảng hoặc chuỗi lớn để tối ưu hóa bộ nhớ động (SRAM).                       | `Hello, PROGMEM!` in Serial Monitor     |
| **`sizeof()`**  | Trả về kích thước (số byte) của biến, mảng, hoặc kiểu dữ liệu.                                    | Kiểm tra kích thước dữ liệu hoặc mảng, tránh lỗi vượt quá phạm vi hoặc tối ưu hóa bộ nhớ chương trình. | `sizeof(int) = 2 bytes`                 |

---

**Lưu ý:**
- **`PROGMEM`** chỉ cần thiết trên các board Arduino với bộ nhớ SRAM hạn chế (như Arduino UNO, Nano).
- **`sizeof()`** là công cụ mạnh mẽ để quản lý và tối ưu hóa khi lập trình với mảng hoặc dữ liệu phức tạp.



# Digital I/O

### **Digital I/O trong Arduino**

Digital I/O (Input/Output) là một trong những tính năng cơ bản của Arduino, giúp điều khiển và đọc tín hiệu số từ các chân (pins) trên board. Dưới đây là mô tả, giải thích và ví dụ chi tiết cho từng hàm.

---

### **1. `digitalRead()`**

#### **Mô tả:**
- Hàm dùng để đọc giá trị logic (HIGH hoặc LOW) từ một chân digital đã được thiết lập làm đầu vào (INPUT).

#### **Cú pháp:**
```cpp
int digitalRead(uint8_t pin);
```

#### **Giải thích:**
- Trả về `HIGH` nếu chân có điện áp 5V (hoặc 3.3V trên một số board).
- Trả về `LOW` nếu chân được nối xuống GND hoặc không có tín hiệu.

#### **Ví dụ: Đọc tín hiệu từ một nút nhấn**
```cpp
const int buttonPin = 2;  // Chân kết nối nút nhấn
const int ledPin = 13;    // Chân LED tích hợp

void setup() {
  pinMode(buttonPin, INPUT);  // Thiết lập buttonPin làm INPUT
  pinMode(ledPin, OUTPUT);    // Thiết lập ledPin làm OUTPUT
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút nhấn

  if (buttonState == HIGH) {  // Nếu nút được nhấn
    digitalWrite(ledPin, HIGH);  // Bật LED
  } else {
    digitalWrite(ledPin, LOW);   // Tắt LED
  }
}
```

---

### **2. `digitalWrite()`**

#### **Mô tả:**
- Hàm dùng để ghi giá trị logic (HIGH hoặc LOW) lên một chân digital đã được thiết lập làm đầu ra (OUTPUT).

#### **Cú pháp:**
```cpp
void digitalWrite(uint8_t pin, uint8_t value);
```

#### **Giải thích:**
- **`HIGH`**: Cấp điện áp 5V (hoặc 3.3V) cho chân.
- **`LOW`**: Đưa chân xuống mức điện áp 0V.

#### **Ví dụ: Nhấp nháy LED**
```cpp
const int ledPin = 13;  // Chân LED tích hợp

void setup() {
  pinMode(ledPin, OUTPUT);  // Thiết lập ledPin làm OUTPUT
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Bật LED
  delay(1000);                 // Chờ 1 giây
  digitalWrite(ledPin, LOW);   // Tắt LED
  delay(1000);                 // Chờ 1 giây
}
```

---

### **3. `pinMode()`**

#### **Mô tả:**
- Hàm dùng để cấu hình chức năng của một chân digital (INPUT, OUTPUT, hoặc INPUT_PULLUP).

#### **Cú pháp:**
```cpp
void pinMode(uint8_t pin, uint8_t mode);
```

#### **Giải thích:**
- **`INPUT`**: Thiết lập chân làm đầu vào.
- **`OUTPUT`**: Thiết lập chân làm đầu ra.
- **`INPUT_PULLUP`**: Thiết lập chân làm đầu vào với điện trở pull-up nội bộ.

#### **Ví dụ: Sử dụng điện trở pull-up nội bộ**
```cpp
const int buttonPin = 2;  // Chân kết nối nút nhấn
const int ledPin = 13;    // Chân LED tích hợp

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);  // Sử dụng pull-up nội bộ
  pinMode(ledPin, OUTPUT);          // Thiết lập ledPin làm OUTPUT
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút nhấn

  if (buttonState == LOW) {  // Nút nhấn được kích hoạt (GND)
    digitalWrite(ledPin, HIGH);  // Bật LED
  } else {
    digitalWrite(ledPin, LOW);   // Tắt LED
  }
}
```

---

### **Tóm tắt bảng**

| **Hàm**           | **Mô tả**                                                                                       | **Ứng dụng**                               | **Ví dụ**                              |
|--------------------|------------------------------------------------------------------------------------------------|--------------------------------------------|----------------------------------------|
| **`digitalRead()`** | Đọc trạng thái HIGH hoặc LOW từ một chân digital.                                              | Đọc tín hiệu từ nút nhấn, cảm biến, v.v.    | `digitalRead(buttonPin)`              |
| **`digitalWrite()`** | Ghi tín hiệu HIGH hoặc LOW lên một chân digital.                                              | Điều khiển LED, relay, mô-đun điện tử khác. | `digitalWrite(ledPin, HIGH)`          |
| **`pinMode()`**     | Thiết lập chức năng cho một chân digital: INPUT, OUTPUT, hoặc INPUT_PULLUP.                    | Cấu hình chân cho các thiết bị hoặc tín hiệu.| `pinMode(buttonPin, INPUT_PULLUP)`    |

---

**Lưu ý:**
- **`INPUT_PULLUP`** rất hữu ích khi không muốn sử dụng điện trở ngoài cho nút nhấn.
- Khi thiết lập một chân làm **OUTPUT**, đảm bảo không đấu nối trực tiếp với các thiết bị nhạy cảm mà không có mạch bảo vệ. 



# Digital I/O

### **Digital I/O trong Arduino**

Digital I/O (Input/Output) là một trong những tính năng cơ bản của Arduino, giúp điều khiển và đọc tín hiệu số từ các chân (pins) trên board. Dưới đây là mô tả, giải thích và ví dụ chi tiết cho từng hàm.

---

### **1. `digitalRead()`**

#### **Mô tả:**
- Hàm dùng để đọc giá trị logic (HIGH hoặc LOW) từ một chân digital đã được thiết lập làm đầu vào (INPUT).

#### **Cú pháp:**
```cpp
int digitalRead(uint8_t pin);
```

#### **Giải thích:**
- Trả về `HIGH` nếu chân có điện áp 5V (hoặc 3.3V trên một số board).
- Trả về `LOW` nếu chân được nối xuống GND hoặc không có tín hiệu.

#### **Ví dụ: Đọc tín hiệu từ một nút nhấn**
```cpp
const int buttonPin = 2;  // Chân kết nối nút nhấn
const int ledPin = 13;    // Chân LED tích hợp

void setup() {
  pinMode(buttonPin, INPUT);  // Thiết lập buttonPin làm INPUT
  pinMode(ledPin, OUTPUT);    // Thiết lập ledPin làm OUTPUT
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút nhấn

  if (buttonState == HIGH) {  // Nếu nút được nhấn
    digitalWrite(ledPin, HIGH);  // Bật LED
  } else {
    digitalWrite(ledPin, LOW);   // Tắt LED
  }
}
```

---

### **2. `digitalWrite()`**

#### **Mô tả:**
- Hàm dùng để ghi giá trị logic (HIGH hoặc LOW) lên một chân digital đã được thiết lập làm đầu ra (OUTPUT).

#### **Cú pháp:**
```cpp
void digitalWrite(uint8_t pin, uint8_t value);
```

#### **Giải thích:**
- **`HIGH`**: Cấp điện áp 5V (hoặc 3.3V) cho chân.
- **`LOW`**: Đưa chân xuống mức điện áp 0V.

#### **Ví dụ: Nhấp nháy LED**
```cpp
const int ledPin = 13;  // Chân LED tích hợp

void setup() {
  pinMode(ledPin, OUTPUT);  // Thiết lập ledPin làm OUTPUT
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Bật LED
  delay(1000);                 // Chờ 1 giây
  digitalWrite(ledPin, LOW);   // Tắt LED
  delay(1000);                 // Chờ 1 giây
}
```

---

### **3. `pinMode()`**

#### **Mô tả:**
- Hàm dùng để cấu hình chức năng của một chân digital (INPUT, OUTPUT, hoặc INPUT_PULLUP).

#### **Cú pháp:**
```cpp
void pinMode(uint8_t pin, uint8_t mode);
```

#### **Giải thích:**
- **`INPUT`**: Thiết lập chân làm đầu vào.
- **`OUTPUT`**: Thiết lập chân làm đầu ra.
- **`INPUT_PULLUP`**: Thiết lập chân làm đầu vào với điện trở pull-up nội bộ.

#### **Ví dụ: Sử dụng điện trở pull-up nội bộ**
```cpp
const int buttonPin = 2;  // Chân kết nối nút nhấn
const int ledPin = 13;    // Chân LED tích hợp

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);  // Sử dụng pull-up nội bộ
  pinMode(ledPin, OUTPUT);          // Thiết lập ledPin làm OUTPUT
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // Đọc trạng thái nút nhấn

  if (buttonState == LOW) {  // Nút nhấn được kích hoạt (GND)
    digitalWrite(ledPin, HIGH);  // Bật LED
  } else {
    digitalWrite(ledPin, LOW);   // Tắt LED
  }
}
```

---

### **Tóm tắt bảng**

| **Hàm**           | **Mô tả**                                                                                       | **Ứng dụng**                               | **Ví dụ**                              |
|--------------------|------------------------------------------------------------------------------------------------|--------------------------------------------|----------------------------------------|
| **`digitalRead()`** | Đọc trạng thái HIGH hoặc LOW từ một chân digital.                                              | Đọc tín hiệu từ nút nhấn, cảm biến, v.v.    | `digitalRead(buttonPin)`              |
| **`digitalWrite()`** | Ghi tín hiệu HIGH hoặc LOW lên một chân digital.                                              | Điều khiển LED, relay, mô-đun điện tử khác. | `digitalWrite(ledPin, HIGH)`          |
| **`pinMode()`**     | Thiết lập chức năng cho một chân digital: INPUT, OUTPUT, hoặc INPUT_PULLUP.                    | Cấu hình chân cho các thiết bị hoặc tín hiệu.| `pinMode(buttonPin, INPUT_PULLUP)`    |

---

**Lưu ý:**
- **`INPUT_PULLUP`** rất hữu ích khi không muốn sử dụng điện trở ngoài cho nút nhấn.
- Khi thiết lập một chân làm **OUTPUT**, đảm bảo không đấu nối trực tiếp với các thiết bị nhạy cảm mà không có mạch bảo vệ. 



# Math
### **Math Functions trong Arduino**

Arduino cung cấp các hàm toán học giúp xử lý dữ liệu số một cách dễ dàng và hiệu quả. Dưới đây là danh sách các hàm phổ biến như `abs()`, `constrain()`, `map()`, `max()`, `min()`, `pow()`, `sq()`, và `sqrt()` cùng mô tả, giải thích và ví dụ.

---

### **1. `abs()`**

#### **Mô tả:**
- Trả về giá trị tuyệt đối của một số.

#### **Cú pháp:**
```cpp
int abs(int x);
float abs(float x);  // Tùy kiểu dữ liệu
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int x = -10;
  Serial.println(abs(x));  // In ra: 10
}

void loop() {}
```

---

### **2. `constrain()`**

#### **Mô tả:**
- Giới hạn giá trị đầu vào trong một khoảng cho trước.

#### **Cú pháp:**
```cpp
int constrain(int x, int a, int b);
```

#### **Giải thích:**
- Nếu `x` nhỏ hơn `a`, trả về `a`.
- Nếu `x` lớn hơn `b`, trả về `b`.
- Nếu `x` nằm giữa `a` và `b`, trả về `x`.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int value = 120;
  Serial.println(constrain(value, 0, 100));  // In ra: 100
}

void loop() {}
```

---

### **3. `map()`**

#### **Mô tả:**
- Chuyển đổi một giá trị từ phạm vi này sang phạm vi khác.

#### **Cú pháp:**
```cpp
long map(long x, long in_min, long in_max, long out_min, long out_max);
```

#### **Giải thích:**
- `x` là giá trị cần chuyển đổi.
- `in_min`, `in_max`: Phạm vi gốc.
- `out_min`, `out_max`: Phạm vi mục tiêu.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int sensorValue = 512;  // Giá trị từ 0-1023
  int mappedValue = map(sensorValue, 0, 1023, 0, 100);  // Chuyển sang 0-100
  Serial.println(mappedValue);  // In ra: 50
}

void loop() {}
```

---

### **4. `max()`**

#### **Mô tả:**
- Trả về giá trị lớn hơn giữa hai số.

#### **Cú pháp:**
```cpp
int max(int a, int b);
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int a = 5, b = 10;
  Serial.println(max(a, b));  // In ra: 10
}

void loop() {}
```

---

### **5. `min()`**

#### **Mô tả:**
- Trả về giá trị nhỏ hơn giữa hai số.

#### **Cú pháp:**
```cpp
int min(int a, int b);
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int a = 5, b = 10;
  Serial.println(min(a, b));  // In ra: 5
}

void loop() {}
```

---

### **6. `pow()`**

#### **Mô tả:**
- Tính lũy thừa của một số.

#### **Cú pháp:**
```cpp
double pow(double base, double exponent);
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  double result = pow(2, 3);  // 2^3 = 8
  Serial.println(result);     // In ra: 8
}

void loop() {}
```

---

### **7. `sq()`**

#### **Mô tả:**
- Tính bình phương của một số.

#### **Cú pháp:**
```cpp
int sq(int x);
float sq(float x);
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int x = 4;
  Serial.println(sq(x));  // In ra: 16
}

void loop() {}
```

---

### **8. `sqrt()`**

#### **Mô tả:**
- Tính căn bậc hai của một số.

#### **Cú pháp:**
```cpp
double sqrt(double x);
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  double x = 16;
  Serial.println(sqrt(x));  // In ra: 4
}

void loop() {}
```

---

### **Tóm tắt bảng**

| **Hàm**         | **Mô tả**                                                            | **Ví dụ**                | **Kết quả**      |
|------------------|----------------------------------------------------------------------|--------------------------|------------------|
| **`abs()`**     | Trả về giá trị tuyệt đối.                                            | `abs(-10)`               | 10               |
| **`constrain()`** | Giới hạn giá trị trong khoảng cho trước.                            | `constrain(120, 0, 100)` | 100              |
| **`map()`**     | Chuyển đổi giá trị giữa hai phạm vi.                                 | `map(512, 0, 1023, 0, 100)` | 50              |
| **`max()`**     | Trả về giá trị lớn hơn giữa hai số.                                  | `max(5, 10)`             | 10               |
| **`min()`**     | Trả về giá trị nhỏ hơn giữa hai số.                                  | `min(5, 10)`             | 5                |
| **`pow()`**     | Tính lũy thừa của một số.                                           | `pow(2, 3)`              | 8                |
| **`sq()`**      | Tính bình phương của một số.                                        | `sq(4)`                  | 16               |
| **`sqrt()`**    | Tính căn bậc hai của một số.                                        | `sqrt(16)`               | 4                |

---



# Bits and Bytes

### **Bits and Bytes trong Arduino**

Arduino cung cấp các hàm để làm việc với bit và byte. Dưới đây là mô tả, giải thích, và ví dụ về các hàm như `bit()`, `bitClear()`, `bitRead()`, `bitSet()`, `bitWrite()`, `highByte()`, và `lowByte()`.

---

### **1. `bit()`**

#### **Mô tả:**
- Tạo ra một giá trị với một bit duy nhất được bật (1) tại vị trí được chỉ định.

#### **Cú pháp:**
```cpp
unsigned int bit(int n);
```

#### **Giải thích:**
- `n`: Vị trí bit (bắt đầu từ 0).
- Trả về giá trị dạng số nguyên với bit thứ `n` được bật.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  Serial.println(bit(3), BIN);  // In ra: 1000
}

void loop() {}
```

---

### **2. `bitClear()`**

#### **Mô tả:**
- Xóa (đặt thành 0) một bit cụ thể trong giá trị.

#### **Cú pháp:**
```cpp
bitClear(x, n);
```

#### **Giải thích:**
- `x`: Giá trị ban đầu.
- `n`: Vị trí bit cần xóa.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  byte x = 0b1111;  // 15 trong nhị phân
  bitClear(x, 2);   // Xóa bit thứ 2
  Serial.println(x, BIN);  // In ra: 1011
}

void loop() {}
```

---

### **3. `bitRead()`**

#### **Mô tả:**
- Đọc giá trị (0 hoặc 1) của một bit tại vị trí chỉ định.

#### **Cú pháp:**
```cpp
bitRead(x, n);
```

#### **Giải thích:**
- `x`: Giá trị cần đọc.
- `n`: Vị trí bit cần đọc.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  byte x = 0b1010;  // Giá trị nhị phân
  Serial.println(bitRead(x, 1));  // In ra: 1
  Serial.println(bitRead(x, 0));  // In ra: 0
}

void loop() {}
```

---

### **4. `bitSet()`**

#### **Mô tả:**
- Bật (đặt thành 1) một bit cụ thể trong giá trị.

#### **Cú pháp:**
```cpp
bitSet(x, n);
```

#### **Giải thích:**
- `x`: Giá trị ban đầu.
- `n`: Vị trí bit cần bật.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  byte x = 0b0000;  // 0 trong nhị phân
  bitSet(x, 2);     // Bật bit thứ 2
  Serial.println(x, BIN);  // In ra: 100
}

void loop() {}
```

---

### **5. `bitWrite()`**

#### **Mô tả:**
- Ghi giá trị (0 hoặc 1) vào một bit cụ thể trong giá trị.

#### **Cú pháp:**
```cpp
bitWrite(x, n, b);
```

#### **Giải thích:**
- `x`: Giá trị ban đầu.
- `n`: Vị trí bit cần ghi.
- `b`: Giá trị cần ghi (0 hoặc 1).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  byte x = 0b1010;  // Giá trị ban đầu
  bitWrite(x, 1, 0); // Ghi giá trị 0 vào bit thứ 1
  Serial.println(x, BIN);  // In ra: 1000
}

void loop() {}
```

---

### **6. `highByte()`**

#### **Mô tả:**
- Trích xuất byte cao (high byte) từ một giá trị 16-bit.

#### **Cú pháp:**
```cpp
byte highByte(int x);
```

#### **Giải thích:**
- Trả về byte cao (8 bit bên trái) của giá trị 16-bit.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int x = 0xABCD;  // Hexadecimal
  Serial.println(highByte(x), HEX);  // In ra: AB
}

void loop() {}
```

---

### **7. `lowByte()`**

#### **Mô tả:**
- Trích xuất byte thấp (low byte) từ một giá trị 16-bit.

#### **Cú pháp:**
```cpp
byte lowByte(int x);
```

#### **Giải thích:**
- Trả về byte thấp (8 bit bên phải) của giá trị 16-bit.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  int x = 0xABCD;  // Hexadecimal
  Serial.println(lowByte(x), HEX);  // In ra: CD
}

void loop() {}
```

---

### **Tóm tắt bảng**

| **Hàm**         | **Mô tả**                                                 | **Ví dụ**                              | **Kết quả**   |
|------------------|-----------------------------------------------------------|----------------------------------------|---------------|
| **`bit()`**     | Bật một bit tại vị trí chỉ định.                           | `bit(3)`                              | 8 (1000)      |
| **`bitClear()`** | Xóa một bit cụ thể trong giá trị.                         | `bitClear(15, 2)`                     | 11 (1011)     |
| **`bitRead()`** | Đọc giá trị của một bit tại vị trí chỉ định.               | `bitRead(10, 1)`                      | 1             |
| **`bitSet()`**  | Bật một bit cụ thể trong giá trị.                         | `bitSet(0, 2)`                        | 4 (100)       |
| **`bitWrite()`** | Ghi giá trị (0 hoặc 1) vào một bit cụ thể.                | `bitWrite(10, 1, 0)`                  | 8 (1000)      |
| **`highByte()`**| Lấy byte cao từ giá trị 16-bit.                           | `highByte(0xABCD)`                    | 0xAB          |
| **`lowByte()`** | Lấy byte thấp từ giá trị 16-bit.                          | `lowByte(0xABCD)`                     | 0xCD          |

---



# Analog I/O

### **Analog I/O trong Arduino**

Arduino hỗ trợ các hàm đọc và ghi tín hiệu analog để giao tiếp với các cảm biến và thiết bị ngoại vi. Dưới đây là mô tả, giải thích và ví dụ về các hàm liên quan đến Analog I/O.

---

### **1. `analogRead()`**

#### **Mô tả:**
- Đọc giá trị điện áp từ một chân analog (các chân được đánh dấu A0, A1,...).
- Giá trị trả về nằm trong khoảng từ 0 đến 1023 (mặc định), tương ứng với điện áp từ 0V đến 5V (hoặc 3.3V tùy vào board Arduino).

#### **Cú pháp:**
```cpp
int analogRead(pin);
```

#### **Giải thích:**
- `pin`: Chân analog muốn đọc (A0, A1,...).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(A0);  // Đọc giá trị từ chân A0
  Serial.println(sensorValue);      // In giá trị đọc được
  delay(500);
}
```

---

### **2. `analogReadResolution()`**

#### **Mô tả:**
- Thiết lập độ phân giải (số bit) cho giá trị đọc từ chân analog.

#### **Cú pháp:**
```cpp
analogReadResolution(bits);
```

#### **Giải thích:**
- `bits`: Số bit độ phân giải (mặc định là 10, tương ứng với giá trị 0–1023).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  analogReadResolution(12);  // Thiết lập độ phân giải 12 bit (0–4095)
}

void loop() {
  int sensorValue = analogRead(A0);  // Đọc giá trị từ chân A0
  Serial.println(sensorValue);      // In giá trị đọc được
  delay(500);
}
```

---

### **3. `analogReference()`**

#### **Mô tả:**
- Chọn điện áp tham chiếu để sử dụng trong việc đọc tín hiệu analog.

#### **Cú pháp:**
```cpp
analogReference(type);
```

#### **Giải thích:**
- `type`: Loại điện áp tham chiếu:
  - `DEFAULT`: Điện áp mặc định (5V hoặc 3.3V).
  - `INTERNAL`: Điện áp tham chiếu bên trong (1.1V cho một số board Arduino).
  - `EXTERNAL`: Điện áp tham chiếu từ chân AREF.

#### **Ví dụ:**
```cpp
void setup() {
  analogReference(DEFAULT);  // Sử dụng điện áp tham chiếu mặc định
}

void loop() {}
```

---

### **4. `analogWrite()`**

#### **Mô tả:**
- Gửi tín hiệu PWM (giả analog) đến một chân số hỗ trợ PWM (các chân có ký hiệu `~`).

#### **Cú pháp:**
```cpp
analogWrite(pin, value);
```

#### **Giải thích:**
- `pin`: Chân PWM muốn ghi tín hiệu.
- `value`: Giá trị từ 0 (0% PWM) đến 255 (100% PWM).

#### **Ví dụ:**
```cpp
void setup() {
  pinMode(9, OUTPUT);  // Chân 9 là chân PWM
}

void loop() {
  analogWrite(9, 128);  // Gửi tín hiệu 50% PWM đến chân 9
  delay(1000);
  analogWrite(9, 255);  // Gửi tín hiệu 100% PWM
  delay(1000);
}
```

---

### **5. `analogWriteResolution()`**

#### **Mô tả:**
- Thiết lập độ phân giải (số bit) cho tín hiệu PWM gửi đi.

#### **Cú pháp:**
```cpp
analogWriteResolution(bits);
```

#### **Giải thích:**
- `bits`: Số bit độ phân giải (mặc định là 8, tương ứng với giá trị từ 0–255).

#### **Ví dụ:**
```cpp
void setup() {
  analogWriteResolution(10);  // Thiết lập độ phân giải PWM là 10 bit (0–1023)
  analogWrite(9, 512);        // Gửi tín hiệu PWM 50%
}

void loop() {}
```

---

### **Tóm tắt bảng**

| **Hàm**                     | **Mô tả**                                                                                       | **Ví dụ**                                           | **Kết quả**                             |
|------------------------------|------------------------------------------------------------------------------------------------|----------------------------------------------------|-----------------------------------------|
| **`analogRead()`**           | Đọc tín hiệu analog từ một chân analog.                                                       | `analogRead(A0)`                                   | Trả về giá trị từ 0–1023 (hoặc tùy độ phân giải). |
| **`analogReadResolution()`** | Thiết lập độ phân giải của tín hiệu đọc từ chân analog.                                        | `analogReadResolution(12)`                        | Đọc giá trị từ 0–4095 (12-bit).         |
| **`analogReference()`**      | Thiết lập điện áp tham chiếu cho tín hiệu analog.                                              | `analogReference(DEFAULT)`                        | Sử dụng điện áp mặc định (5V hoặc 3.3V).|
| **`analogWrite()`**          | Gửi tín hiệu PWM đến một chân số hỗ trợ PWM.                                                  | `analogWrite(9, 128)`                             | Tín hiệu PWM 50% (128/255).             |
| **`analogWriteResolution()`**| Thiết lập độ phân giải của tín hiệu PWM.                                                      | `analogWriteResolution(10)`                       | PWM giá trị từ 0–1023 (10-bit).         |

---



# Trigonometry

### **Trigonometry Functions trong Arduino**

Arduino cung cấp các hàm lượng giác để thực hiện các phép tính toán học liên quan đến góc, rất hữu ích trong các ứng dụng như điều khiển servo, vẽ đồ họa, hoặc tính toán các hệ tọa độ.

---

### **1. `cos()`**

#### **Mô tả:**
- Tính giá trị cosin của một góc (theo radian).

#### **Cú pháp:**
```cpp
double cos(double radians);
```

#### **Giải thích:**
- **`radians`**: Góc được nhập vào theo đơn vị radian.
- Trả về giá trị cosin, nằm trong khoảng từ -1 đến 1.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  double angle = 3.14159 / 3;  // Góc 60 độ, chuyển sang radian
  double cosValue = cos(angle);
  Serial.println(cosValue);    // Kết quả gần bằng 0.5
}

void loop() {}
```

---

### **2. `sin()`**

#### **Mô tả:**
- Tính giá trị sin của một góc (theo radian).

#### **Cú pháp:**
```cpp
double sin(double radians);
```

#### **Giải thích:**
- **`radians`**: Góc được nhập vào theo đơn vị radian.
- Trả về giá trị sin, nằm trong khoảng từ -1 đến 1.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  double angle = 3.14159 / 2;  // Góc 90 độ, chuyển sang radian
  double sinValue = sin(angle);
  Serial.println(sinValue);    // Kết quả gần bằng 1.0
}

void loop() {}
```

---

### **3. `tan()`**

#### **Mô tả:**
- Tính giá trị tang của một góc (theo radian).

#### **Cú pháp:**
```cpp
double tan(double radians);
```

#### **Giải thích:**
- **`radians`**: Góc được nhập vào theo đơn vị radian.
- Trả về giá trị tang (có thể lớn hơn 1 hoặc nhỏ hơn -1, tùy góc).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  double angle = 3.14159 / 4;  // Góc 45 độ, chuyển sang radian
  double tanValue = tan(angle);
  Serial.println(tanValue);    // Kết quả gần bằng 1.0
}

void loop() {}
```

---

### **Tóm tắt bảng**

| **Hàm** | **Mô tả**                                   | **Cú pháp**            | **Kết quả** |
|---------|---------------------------------------------|-------------------------|-------------|
| `cos()` | Tính cosin của góc (radian).                | `cos(3.14 / 3)`         | Gần bằng 0.5|
| `sin()` | Tính sin của góc (radian).                  | `sin(3.14 / 2)`         | Gần bằng 1.0|
| `tan()` | Tính tang của góc (radian).                 | `tan(3.14 / 4)`         | Gần bằng 1.0|

---

### **Chuyển đổi độ sang radian**

- Trong Arduino, góc thường phải được nhập theo **radian**.
- Công thức chuyển đổi:
  \[
  \text{Radian} = \text{Degree} \times \frac{\pi}{180}
  \]

#### **Ví dụ chuyển đổi góc 90 độ sang radian:**
```cpp
double radians = 90 * 3.14159 / 180;  // Kết quả: 1.5708 radian
```

---

### **Ứng dụng thực tế:**
#### **Điều khiển servo với lượng giác**
```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9);
}

void loop() {
  for (int angle = 0; angle <= 180; angle++) {
    double radians = angle * 3.14159 / 180;
    int position = 90 + (cos(radians) * 45);  // Vị trí từ 45 đến 135 độ
    myServo.write(position);
    delay(15);
  }
}
```

---



# External Interrupts

### **External Interrupts trong Arduino**

Interrupts (ngắt) là cơ chế cho phép một chương trình dừng công việc hiện tại để xử lý một sự kiện cụ thể, sau đó quay lại công việc ban đầu. Arduino hỗ trợ **external interrupts** để phản hồi nhanh với các tín hiệu từ bên ngoài, chẳng hạn như nút nhấn hoặc cảm biến.

---

### **1. `attachInterrupt()`**

#### **Mô tả:**
- Gắn một hàm xử lý ngắt vào một chân cụ thể.

#### **Cú pháp:**
```cpp
attachInterrupt(digitalPinToInterrupt(pin), ISR, mode);
```

#### **Giải thích:**
- **`digitalPinToInterrupt(pin)`**: Chuyển đổi chân digital thành số interrupt (tùy thuộc vào board Arduino).
- **`ISR`**: Tên hàm sẽ được gọi khi ngắt xảy ra (**Interrupt Service Routine**).
- **`mode`**:
  - `LOW`: Gọi ISR khi tín hiệu ở mức thấp.
  - `CHANGE`: Gọi ISR khi tín hiệu thay đổi (từ LOW sang HIGH hoặc ngược lại).
  - `RISING`: Gọi ISR khi tín hiệu chuyển từ LOW sang HIGH.
  - `FALLING`: Gọi ISR khi tín hiệu chuyển từ HIGH sang LOW.

#### **Ví dụ:**
```cpp
volatile int counter = 0;  // Biến được sử dụng trong ngắt phải là `volatile`.

void setup() {
  pinMode(2, INPUT_PULLUP);  // Cấu hình chân 2 làm INPUT với PULLUP
  attachInterrupt(digitalPinToInterrupt(2), incrementCounter, RISING);
  Serial.begin(9600);
}

void loop() {
  Serial.println(counter);
  delay(1000);
}

void incrementCounter() {
  counter++;
}
```

---

### **2. `detachInterrupt()`**

#### **Mô tả:**
- Hủy bỏ ngắt trên một chân cụ thể.

#### **Cú pháp:**
```cpp
detachInterrupt(digitalPinToInterrupt(pin));
```

#### **Giải thích:**
- Sau khi gọi `detachInterrupt()`, Arduino sẽ không xử lý ngắt cho chân đó nữa.

#### **Ví dụ:**
```cpp
void setup() {
  pinMode(2, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(2), toggleLED, RISING);
  pinMode(13, OUTPUT);
}

void loop() {
  delay(5000);
  detachInterrupt(digitalPinToInterrupt(2));  // Hủy bỏ ngắt sau 5 giây
}

void toggleLED() {
  digitalWrite(13, !digitalRead(13));
}
```

---

### **3. `digitalPinToInterrupt()`**

#### **Mô tả:**
- Trả về số interrupt tương ứng với một chân digital trên Arduino.

#### **Cú pháp:**
```cpp
int interruptNumber = digitalPinToInterrupt(pin);
```

#### **Giải thích:**
- Sử dụng khi bạn cần biết số interrupt của một chân digital.

#### **Ví dụ:**
```cpp
void setup() {
  int interruptNum = digitalPinToInterrupt(2);
  Serial.begin(9600);
  Serial.print("Interrupt number for pin 2: ");
  Serial.println(interruptNum);
}
```

---

### **Tóm tắt bảng**

| **Hàm**                  | **Mô tả**                                                                                | **Cú pháp**                                                                  |
|--------------------------|------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| `attachInterrupt()`      | Gắn hàm xử lý ngắt cho một chân.                                                         | `attachInterrupt(digitalPinToInterrupt(pin), ISR, mode);`                   |
| `detachInterrupt()`      | Hủy bỏ ngắt trên một chân.                                                               | `detachInterrupt(digitalPinToInterrupt(pin));`                              |
| `digitalPinToInterrupt()`| Trả về số interrupt của một chân digital.                                                | `int interruptNum = digitalPinToInterrupt(pin);`                            |

---

### **Ứng dụng thực tế:**

#### **Đếm số lần nhấn nút:**
```cpp
volatile int buttonPresses = 0;

void setup() {
  pinMode(2, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(2), countPress, FALLING);
  Serial.begin(9600);
}

void loop() {
  Serial.print("Button presses: ");
  Serial.println(buttonPresses);
  delay(1000);
}

void countPress() {
  buttonPresses++;
}
```

#### **Tạm dừng ngắt trong một khoảng thời gian:**
```cpp
volatile bool state = false;

void setup() {
  pinMode(2, INPUT_PULLUP);
  pinMode(13, OUTPUT);
  attachInterrupt(digitalPinToInterrupt(2), toggleState, CHANGE);
}

void loop() {
  digitalWrite(13, state);
  delay(5000);
  detachInterrupt(digitalPinToInterrupt(2));  // Hủy ngắt
  delay(5000);
  attachInterrupt(digitalPinToInterrupt(2), toggleState, CHANGE);  // Kích hoạt lại
}

void toggleState() {
  state = !state;
}
```

---

Interrupts giúp Arduino xử lý các sự kiện quan trọng một cách tức thời, ngay cả khi chương trình đang bận thực hiện các nhiệm vụ khác.

# Advanced I/O

### **Advanced I/O trong Arduino**

Các hàm Advanced I/O cung cấp khả năng điều khiển các tín hiệu I/O đặc biệt, chẳng hạn như tạo âm thanh, đo xung, hoặc giao tiếp nối tiếp cơ bản bằng các chân digital.

---

### **1. `noTone()`**

#### **Mô tả:**
Dừng việc tạo tín hiệu âm thanh (tone) trên một chân đã được sử dụng bởi `tone()`.

#### **Cú pháp:**
```cpp
noTone(pin);
```

#### **Tham số:**
- **`pin`**: Chân digital nơi âm thanh đang được phát.

#### **Ví dụ:**
```cpp
void setup() {
  tone(8, 1000);  // Tạo âm tần số 1000 Hz trên chân 8
  delay(2000);    // Phát âm trong 2 giây
  noTone(8);      // Dừng phát âm
}

void loop() {
}
```

---

### **2. `pulseIn()`**

#### **Mô tả:**
Đo thời gian của một xung HIGH hoặc LOW trên một chân.

#### **Cú pháp:**
```cpp
unsigned long duration = pulseIn(pin, value, timeout);
```

#### **Tham số:**
- **`pin`**: Chân digital cần đo xung.
- **`value`**: Mức tín hiệu cần đo (HIGH hoặc LOW).
- **`timeout`** *(tùy chọn)*: Thời gian tối đa chờ tín hiệu, tính bằng micro giây.

#### **Trả về:**
Thời gian của xung (micro giây) hoặc 0 nếu vượt quá `timeout`.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  pinMode(7, INPUT);
}

void loop() {
  unsigned long duration = pulseIn(7, HIGH);
  Serial.print("Pulse duration: ");
  Serial.print(duration);
  Serial.println(" microseconds");
}
```

---

### **3. `pulseInLong()`**

#### **Mô tả:**
Tương tự `pulseIn()`, nhưng có độ chính xác cao hơn để đo xung dài.

#### **Cú pháp:**
```cpp
unsigned long duration = pulseInLong(pin, value, timeout);
```

#### **Tham số:**
Giống `pulseIn()`.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  pinMode(7, INPUT);
}

void loop() {
  unsigned long duration = pulseInLong(7, HIGH);
  Serial.print("Long pulse duration: ");
  Serial.print(duration);
  Serial.println(" microseconds");
}
```

---

### **4. `shiftIn()`**

#### **Mô tả:**
Đọc dữ liệu nối tiếp (serial data) từ một chân digital, một bit mỗi lần.

#### **Cú pháp:**
```cpp
byte data = shiftIn(dataPin, clockPin, bitOrder);
```

#### **Tham số:**
- **`dataPin`**: Chân nhận dữ liệu nối tiếp.
- **`clockPin`**: Chân tạo xung clock.
- **`bitOrder`**: Thứ tự bit (LSBFIRST hoặc MSBFIRST).

#### **Ví dụ:**
```cpp
void setup() {
  pinMode(2, INPUT);
  pinMode(3, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  byte data = shiftIn(2, 3, LSBFIRST);
  Serial.println(data);
}
```

---

### **5. `shiftOut()`**

#### **Mô tả:**
Gửi dữ liệu nối tiếp (serial data) tới một chân digital, một bit mỗi lần.

#### **Cú pháp:**
```cpp
shiftOut(dataPin, clockPin, bitOrder, value);
```

#### **Tham số:**
- **`dataPin`**: Chân gửi dữ liệu nối tiếp.
- **`clockPin`**: Chân tạo xung clock.
- **`bitOrder`**: Thứ tự bit (LSBFIRST hoặc MSBFIRST).
- **`value`**: Giá trị byte cần gửi.

#### **Ví dụ:**
```cpp
void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
}

void loop() {
  shiftOut(2, 3, MSBFIRST, 0b10101010);  // Gửi dữ liệu
  delay(1000);
}
```

---

### **6. `tone()`**

#### **Mô tả:**
Phát tín hiệu âm thanh (tone) với tần số và thời gian cụ thể.

#### **Cú pháp:**
```cpp
tone(pin, frequency, duration);
```

#### **Tham số:**
- **`pin`**: Chân phát tín hiệu âm thanh.
- **`frequency`**: Tần số của âm thanh (Hz).
- **`duration`** *(tùy chọn)*: Thời gian phát âm (millisecond).

#### **Ví dụ:**
```cpp
void setup() {
  tone(8, 500);   // Phát âm tần số 500 Hz trên chân 8
  delay(2000);    // Dừng sau 2 giây
  noTone(8);      // Dừng tone
}

void loop() {
}
```

---

### **Tóm tắt bảng**

| **Hàm**          | **Mô tả**                                                                 | **Cú pháp**                                  |
|-------------------|---------------------------------------------------------------------------|----------------------------------------------|
| `noTone()`        | Dừng phát tín hiệu âm thanh trên một chân.                               | `noTone(pin);`                               |
| `pulseIn()`       | Đo thời gian của xung HIGH hoặc LOW.                                     | `pulseIn(pin, value, timeout);`             |
| `pulseInLong()`   | Đo thời gian xung dài với độ chính xác cao.                              | `pulseInLong(pin, value, timeout);`         |
| `shiftIn()`       | Đọc dữ liệu nối tiếp từ chân digital (1 bit/lần).                        | `shiftIn(dataPin, clockPin, bitOrder);`     |
| `shiftOut()`      | Gửi dữ liệu nối tiếp tới chân digital (1 bit/lần).                       | `shiftOut(dataPin, clockPin, bitOrder, val);` |
| `tone()`          | Phát tín hiệu âm thanh với tần số và thời gian cụ thể.                   | `tone(pin, frequency, duration);`           |

---

### **Ứng dụng thực tế:**
1. **Đo xung cảm biến siêu âm**:
   - Sử dụng `pulseIn()` để đo thời gian tín hiệu phản xạ từ cảm biến siêu âm.
   
2. **Điều khiển LED RGB bằng dữ liệu nối tiếp**:
   - Sử dụng `shiftIn()` và `shiftOut()` để giao tiếp với các IC điều khiển LED.

3. **Tạo âm thanh cảnh báo**:
   - Sử dụng `tone()` để tạo âm báo động hoặc cảnh báo khi có sự kiện.


# Characters

### **Characters Functions trong Arduino**

Các hàm này thuộc nhóm kiểm tra ký tự, giúp xác định loại ký tự trong các chuỗi hoặc dữ liệu. Chúng rất hữu ích khi xử lý văn bản hoặc kiểm tra định dạng dữ liệu.

---

### **1. `isAlpha()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là chữ cái (A-Z hoặc a-z) hay không.

#### **Cú pháp:**
```cpp
isAlpha(c);
```

#### **Tham số:**
- **`c`**: Ký tự cần kiểm tra.

#### **Trả về:**
- **`true`**: Nếu là chữ cái.
- **`false`**: Nếu không phải là chữ cái.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  char c = 'A';
  Serial.println(isAlpha(c)); // true
  Serial.println(isAlpha('1')); // false
}
void loop() {}
```

---

### **2. `isAlphaNumeric()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là chữ cái hoặc chữ số hay không.

#### **Cú pháp:**
```cpp
isAlphaNumeric(c);
```

#### **Trả về:**
- **`true`**: Nếu là chữ cái hoặc chữ số.
- **`false`**: Nếu không phải.

#### **Ví dụ:**
```cpp
char c = '9';
Serial.println(isAlphaNumeric(c)); // true
Serial.println(isAlphaNumeric('%')); // false
```

---

### **3. `isAscii()`**

#### **Mô tả:**
Kiểm tra xem ký tự có thuộc bảng mã ASCII chuẩn (0-127) hay không.

#### **Cú pháp:**
```cpp
isAscii(c);
```

#### **Trả về:**
- **`true`**: Nếu thuộc bảng ASCII.
- **`false`**: Nếu không thuộc.

#### **Ví dụ:**
```cpp
Serial.println(isAscii(65)); // true (ký tự 'A')
Serial.println(isAscii(200)); // false
```

---

### **4. `isControl()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là ký tự điều khiển (Control Characters) hay không.

#### **Cú pháp:**
```cpp
isControl(c);
```

#### **Ví dụ:**
```cpp
Serial.println(isControl('\n')); // true
Serial.println(isControl('A')); // false
```

---

### **5. `isDigit()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là chữ số (0-9) hay không.

#### **Ví dụ:**
```cpp
Serial.println(isDigit('5')); // true
Serial.println(isDigit('A')); // false
```

---

### **6. `isGraph()`**

#### **Mô tả:**
Kiểm tra xem ký tự có thể hiển thị được trên màn hình và không phải là khoảng trắng.

#### **Ví dụ:**
```cpp
Serial.println(isGraph('@')); // true
Serial.println(isGraph(' ')); // false
```

---

### **7. `isHexadecimalDigit()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là ký tự hợp lệ trong hệ thập lục phân (0-9, A-F, a-f).

#### **Ví dụ:**
```cpp
Serial.println(isHexadecimalDigit('F')); // true
Serial.println(isHexadecimalDigit('G')); // false
```

---

### **8. `isLowerCase()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là chữ thường (a-z) hay không.

#### **Ví dụ:**
```cpp
Serial.println(isLowerCase('a')); // true
Serial.println(isLowerCase('A')); // false
```

---

### **9. `isPrintable()`**

#### **Mô tả:**
Kiểm tra xem ký tự có thể in được hay không (bao gồm cả khoảng trắng).

#### **Ví dụ:**
```cpp
Serial.println(isPrintable(' ')); // true
Serial.println(isPrintable('\t')); // false
```

---

### **10. `isPunct()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là dấu câu (punctuation) hay không.

#### **Ví dụ:**
```cpp
Serial.println(isPunct(',')); // true
Serial.println(isPunct('A')); // false
```

---

### **11. `isSpace()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là khoảng trắng hay không (bao gồm ` `, `\t`, `\n`, `\v`, `\f`, `\r`).

#### **Ví dụ:**
```cpp
Serial.println(isSpace(' ')); // true
Serial.println(isSpace('A')); // false
```

---

### **12. `isUpperCase()`**

#### **Mô tả:**
Kiểm tra xem ký tự có phải là chữ in hoa (A-Z) hay không.

#### **Ví dụ:**
```cpp
Serial.println(isUpperCase('A')); // true
Serial.println(isUpperCase('a')); // false
```

---

### **13. `isWhitespace()`**

#### **Mô tả:**
Tương tự `isSpace()`. Kiểm tra khoảng trắng, bao gồm cả ký tự điều khiển cho khoảng cách.

#### **Ví dụ:**
```cpp
Serial.println(isWhitespace(' ')); // true
Serial.println(isWhitespace('\n')); // true
Serial.println(isWhitespace('A')); // false
```

---

### **Tóm tắt bảng**

| **Hàm**                 | **Mô tả**                                                  | **Ví dụ kết quả (với ký tự)**   |
|--------------------------|-----------------------------------------------------------|---------------------------------|
| `isAlpha()`              | Là chữ cái (A-Z, a-z).                                     | `'A' -> true`, `'1' -> false`  |
| `isAlphaNumeric()`       | Là chữ cái hoặc số (A-Z, a-z, 0-9).                        | `'9' -> true`, `'%' -> false`  |
| `isAscii()`              | Thuộc bảng mã ASCII (0-127).                              | `65 -> true`, `200 -> false`   |
| `isControl()`            | Là ký tự điều khiển.                                       | `'\n' -> true`, `'A' -> false` |
| `isDigit()`              | Là chữ số (0-9).                                          | `'5' -> true`, `'A' -> false`  |
| `isGraph()`              | Có thể hiển thị, không phải khoảng trắng.                 | `'@' -> true`, `' ' -> false`  |
| `isHexadecimalDigit()`   | Là ký tự thập lục phân (0-9, A-F, a-f).                   | `'F' -> true`, `'G' -> false`  |
| `isLowerCase()`          | Là chữ thường (a-z).                                      | `'a' -> true`, `'A' -> false`  |
| `isPrintable()`          | Có thể in, bao gồm cả khoảng trắng.                       | `' ' -> true`, `'\t' -> false` |
| `isPunct()`              | Là dấu câu.                                               | `',' -> true`, `'A' -> false`  |
| `isSpace()`              | Là khoảng trắng hoặc ký tự điều khiển liên quan.          | `' ' -> true`, `'A' -> false`  |
| `isUpperCase()`          | Là chữ in hoa (A-Z).                                      | `'A' -> true`, `'a' -> false`  |
| `isWhitespace()`         | Là khoảng trắng, bao gồm `\n`, `\t`, `\r`.                | `'\t' -> true`, `'A' -> false` |

---

### **Ứng dụng thực tế:**
1. **Kiểm tra đầu vào của người dùng**:
   - Xác minh xem ký tự nhập vào có phải là số hoặc chữ cái hợp lệ.
   
2. **Phân loại dữ liệu**:
   - Sử dụng để lọc hoặc phân loại chuỗi ký tự.

3. **Phân tích file text**:
   - Kiểm tra và xử lý ký tự đặc biệt hoặc khoảng trắng trong tài liệu.


# Interrupts
### **Interrupts trong Arduino**

Interrupts là một tính năng quan trọng trong Arduino cho phép thiết bị ngừng tạm thời một chương trình đang thực thi để xử lý một sự kiện cấp bách (interrupt). Điều này giúp bạn xử lý sự kiện quan trọng ngay lập tức mà không cần phải chờ đến khi chương trình hiện tại kết thúc.

### **1. `interrupts()`**

#### **Mô tả:**
- Hàm `interrupts()` được sử dụng để bật lại các ngắt (interrupts). Khi một ngắt bị vô hiệu hóa bằng cách gọi `noInterrupts()`, chương trình sẽ tiếp tục chạy mà không có ngắt.
- Khi gọi `interrupts()`, các ngắt sẽ được kích hoạt lại và chương trình có thể xử lý các sự kiện ngắt nếu cần.

#### **Cú pháp:**
```cpp
interrupts();
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  noInterrupts();  // Vô hiệu hóa các ngắt
  delay(1000);     // Đợi 1 giây
  interrupts();    // Bật lại các ngắt
}

void loop() {
  // Chương trình sẽ tiếp tục sau khi ngắt được bật lại
}
```

#### **Chức năng:**
- Đảm bảo rằng các ngắt được kích hoạt sau khi bị vô hiệu hóa.

---

### **2. `noInterrupts()`**

#### **Mô tả:**
- Hàm `noInterrupts()` được sử dụng để tạm thời vô hiệu hóa các ngắt. Điều này giúp đảm bảo rằng không có ngắt nào sẽ xảy ra trong khi chương trình đang thực thi đoạn mã quan trọng mà bạn không muốn bị gián đoạn.
- Các ngắt sẽ bị vô hiệu hóa cho đến khi bạn gọi lại `interrupts()`.

#### **Cú pháp:**
```cpp
noInterrupts();
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  noInterrupts();  // Vô hiệu hóa các ngắt
  delay(1000);     // Đợi 1 giây mà không có ngắt
}

void loop() {
  // Chương trình sẽ tiếp tục sau khi các ngắt bị vô hiệu hóa
}
```

#### **Chức năng:**
- Dùng để bảo vệ các đoạn mã quan trọng khỏi bị gián đoạn do ngắt.

---

### **Tóm tắt và Ứng dụng**

| **Hàm**        | **Mô tả**                                                     | **Ví dụ sử dụng**                                  |
|----------------|---------------------------------------------------------------|----------------------------------------------------|
| `interrupts()` | Kích hoạt lại các ngắt đã bị vô hiệu hóa.                   | Gọi sau `noInterrupts()` để bật lại ngắt sau khi vô hiệu hóa. |
| `noInterrupts()`| Vô hiệu hóa tất cả các ngắt tạm thời.                        | Dùng khi bạn muốn bảo vệ một đoạn mã khỏi bị ngắt. |

#### **Ứng dụng thực tế**:
1. **Bảo vệ các đoạn mã quan trọng**: Khi bạn đang thực hiện một công việc quan trọng như ghi dữ liệu vào bộ nhớ hoặc điều khiển một thiết bị ngoại vi, có thể sử dụng `noInterrupts()` để ngăn ngừa sự can thiệp từ ngắt.
2. **Đảm bảo đồng bộ hóa**: Khi cần bảo vệ các thao tác cần thực hiện một cách nguyên tử (atomic) mà không muốn bị gián đoạn trong quá trình xử lý, việc vô hiệu hóa ngắt tạm thời bằng `noInterrupts()` và kích hoạt lại bằng `interrupts()` là một cách sử dụng rất hữu ích.

# Time

### **Time Functions trong Arduino**

Arduino cung cấp một số hàm để làm việc với thời gian, giúp lập trình viên thực hiện các tác vụ liên quan đến độ trễ hoặc đo thời gian. Dưới đây là các hàm thời gian cơ bản trong Arduino:

---

### **1. `delay()`**

#### **Mô tả:**
- Hàm `delay()` dùng để tạm dừng chương trình trong một khoảng thời gian nhất định (tính bằng mili giây). 
- Chương trình sẽ ngừng thực thi và không thực hiện bất kỳ tác vụ nào khác trong suốt thời gian delay.

#### **Cú pháp:**
```cpp
delay(ms);
```
- **ms**: Số mili giây (1 giây = 1000 mili giây) mà chương trình sẽ tạm dừng.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  Serial.println("Start");
  delay(1000);  // Delay 1 giây (1000 mili giây)
  Serial.println("End");
}

void loop() {
  // Chương trình sẽ in "Start", chờ 1 giây và sau đó in "End"
}
```

#### **Chức năng:**
- Dừng chương trình trong một khoảng thời gian cố định.

---

### **2. `delayMicroseconds()`**

#### **Mô tả:**
- Hàm `delayMicroseconds()` tạm dừng chương trình trong khoảng thời gian tính bằng micro giây (1 micro giây = 1/1,000,000 giây).
- Phù hợp khi bạn cần độ chính xác cao hơn so với `delay()`.

#### **Cú pháp:**
```cpp
delayMicroseconds(us);
```
- **us**: Số micro giây (1 giây = 1,000,000 micro giây) mà chương trình sẽ tạm dừng.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  Serial.println("Start");
  delayMicroseconds(500);  // Delay 500 micro giây
  Serial.println("End");
}

void loop() {
  // Chương trình sẽ in "Start", chờ 500 micro giây và sau đó in "End"
}
```

#### **Chức năng:**
- Dừng chương trình trong thời gian rất ngắn, đạt độ chính xác cao hơn `delay()`.

---

### **3. `micros()`**

#### **Mô tả:**
- Hàm `micros()` trả về số lượng micro giây đã trôi qua từ khi Arduino bắt đầu chạy (tính từ khi board được reset).
- Hàm này hữu ích cho việc đo lường các khoảng thời gian ngắn mà không làm tạm dừng chương trình.

#### **Cú pháp:**
```cpp
unsigned long micros();
```
- Trả về số lượng micro giây dưới dạng giá trị kiểu `unsigned long`.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  unsigned long startTime = micros();  // Lấy thời gian bắt đầu
  delay(1000);  // Đợi 1 giây
  unsigned long elapsedTime = micros() - startTime;  // Tính thời gian đã trôi qua
  Serial.print("Elapsed time: ");
  Serial.println(elapsedTime);  // In ra thời gian trôi qua (tính bằng micro giây)
}

void loop() {
  // In thời gian trôi qua kể từ khi chương trình bắt đầu
}
```

#### **Chức năng:**
- Đo khoảng thời gian ngắn và trả về số lượng micro giây đã trôi qua.

---

### **4. `millis()`**

#### **Mô tả:**
- Hàm `millis()` trả về số lượng mili giây đã trôi qua kể từ khi chương trình bắt đầu (kể từ khi board được reset).
- Đây là một hàm rất hữu ích khi bạn muốn theo dõi thời gian trôi qua mà không cần làm gián đoạn chương trình, đặc biệt trong các ứng dụng liên quan đến thời gian.

#### **Cú pháp:**
```cpp
unsigned long millis();
```
- Trả về số lượng mili giây dưới dạng giá trị kiểu `unsigned long`.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  unsigned long startTime = millis();  // Lấy thời gian bắt đầu
  delay(1000);  // Đợi 1 giây
  unsigned long elapsedTime = millis() - startTime;  // Tính thời gian đã trôi qua
  Serial.print("Elapsed time: ");
  Serial.println(elapsedTime);  // In ra thời gian trôi qua (tính bằng mili giây)
}

void loop() {
  // In thời gian trôi qua kể từ khi chương trình bắt đầu
}
```

#### **Chức năng:**
- Theo dõi thời gian trôi qua từ khi chương trình bắt đầu mà không làm gián đoạn các tác vụ khác trong chương trình.

---

### **Tóm tắt và Ứng dụng**

| **Hàm**                | **Mô tả**                                                   | **Ví dụ sử dụng**                                  |
|------------------------|-------------------------------------------------------------|----------------------------------------------------|
| `delay()`              | Tạm dừng chương trình trong một khoảng thời gian tính bằng mili giây. | Tạm dừng 1 giây, sau đó thực thi chương trình. |
| `delayMicroseconds()`  | Tạm dừng chương trình trong khoảng thời gian tính bằng micro giây. | Tạm dừng 500 micro giây. |
| `micros()`             | Trả về số micro giây đã trôi qua từ khi bắt đầu chương trình. | Đo thời gian từ khi bắt đầu chương trình đến thời điểm hiện tại. |
| `millis()`             | Trả về số mili giây đã trôi qua từ khi bắt đầu chương trình. | Đo thời gian đã trôi qua kể từ khi chương trình bắt đầu mà không gián đoạn. |

#### **Ứng dụng thực tế**:
1. **Đo thời gian thực thi**: Dùng `millis()` hoặc `micros()` để đo thời gian giữa hai sự kiện mà không cần dừng chương trình.
2. **Điều khiển thời gian**: Dùng `delay()` hoặc `delayMicroseconds()` khi cần tạm dừng chương trình trong khoảng thời gian xác định để điều khiển các thiết bị ngoại vi.

# Random Numbers

### **Random Numbers in Arduino**

Arduino provides functions for generating random numbers, which are useful in a variety of applications such as simulations, games, or random behavior generation.

---

### **1. `random()`**

#### **Mô tả:**
- Hàm `random()` trả về một số ngẫu nhiên trong một khoảng xác định.
- Có thể trả về số nguyên trong phạm vi bạn chỉ định hoặc có thể sử dụng hai đối số để chỉ định phạm vi cụ thể.

#### **Cú pháp:**
```cpp
random();
random(min, max);
```
- **`random()`**: Trả về một số ngẫu nhiên trong phạm vi từ 0 đến **2^32 - 1** (tức là từ 0 đến 4,294,967,295).
- **`random(min, max)`**: Trả về một số ngẫu nhiên trong phạm vi từ `min` đến `max - 1`. (Ví dụ: từ 10 đến 20 sẽ trả về các số từ 10 đến 19).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  Serial.println(random());           // Trả về số ngẫu nhiên trong phạm vi 0 đến 4,294,967,295
  Serial.println(random(10, 20));     // Trả về số ngẫu nhiên trong phạm vi 10 đến 19
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Sinh số ngẫu nhiên trong phạm vi từ `min` đến `max - 1`.

---

### **2. `randomSeed()`**

#### **Mô tả:**
- Hàm `randomSeed()` được sử dụng để thiết lập giá trị "hạt giống" (seed) cho hàm `random()`. Bằng cách thay đổi giá trị hạt giống, bạn có thể thay đổi chuỗi các số ngẫu nhiên được sinh ra.
- Nếu không sử dụng `randomSeed()`, Arduino sẽ sử dụng một giá trị hạt giống mặc định, và chuỗi số ngẫu nhiên sẽ luôn giống nhau mỗi lần bạn khởi động lại board Arduino.

#### **Cú pháp:**
```cpp
randomSeed(seed);
```
- **`seed`**: Giá trị hạt giống mà bạn muốn sử dụng để tạo ra chuỗi số ngẫu nhiên. Thông thường, bạn có thể sử dụng một giá trị ngẫu nhiên như giá trị đọc từ một chân đầu vào (ví dụ như đọc giá trị từ một chân analog).

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  randomSeed(analogRead(A0));  // Đặt giá trị hạt giống bằng giá trị ngẫu nhiên từ chân A0
  Serial.println(random(10, 20));  // Trả về số ngẫu nhiên trong phạm vi từ 10 đến 19
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Đặt giá trị hạt giống cho các số ngẫu nhiên, giúp tạo ra chuỗi ngẫu nhiên khác nhau mỗi khi board Arduino được reset.

---

### **Tóm tắt và Ứng dụng**

| **Hàm**         | **Mô tả**                                                 | **Ví dụ sử dụng**                                       |
|-----------------|-----------------------------------------------------------|---------------------------------------------------------|
| `random()`      | Trả về một số ngẫu nhiên trong một phạm vi xác định.       | `random(10, 20)` trả về số ngẫu nhiên trong phạm vi 10 đến 19. |
| `randomSeed()`  | Thiết lập giá trị hạt giống để tạo ra các chuỗi số ngẫu nhiên khác nhau. | `randomSeed(analogRead(A0))` để thiết lập giá trị ngẫu nhiên từ chân A0. |

#### **Ứng dụng thực tế**:
1. **Sinh số ngẫu nhiên**: Dùng để tạo các số ngẫu nhiên trong các trò chơi, mô phỏng hoặc các ứng dụng yêu cầu số ngẫu nhiên.
2. **Thử nghiệm ngẫu nhiên**: Dùng `randomSeed()` kết hợp với một giá trị ngẫu nhiên để tạo ra các chuỗi số ngẫu nhiên khác nhau mỗi khi board được reset, giúp tránh sự trùng lặp trong các số ngẫu nhiên sinh ra.

# Communication
### **Communication Functions in Arduino**

Arduino supports various communication protocols and libraries for communication between the board and other devices. Here are the main communication methods available in Arduino: SPI, Print, Serial, Stream, and Wire.

---

### **1. SPI (Serial Peripheral Interface)**

#### **Mô tả:**
- **SPI** là một giao thức truyền thông đồng bộ sử dụng các dây dữ liệu để giao tiếp giữa một bộ vi điều khiển và các thiết bị ngoại vi (như cảm biến, bộ nhớ, v.v.).
- SPI sử dụng 4 chân chính: **MOSI (Master Out Slave In)**, **MISO (Master In Slave Out)**, **SCK (Serial Clock)**, và **SS (Slave Select)**.

#### **Cú pháp cơ bản:**
```cpp
#include <SPI.h>

SPI.begin();
SPI.transfer(data);
SPI.end();
```

- **`SPI.begin()`**: Khởi tạo giao tiếp SPI.
- **`SPI.transfer(data)`**: Gửi và nhận dữ liệu qua giao thức SPI.
- **`SPI.end()`**: Đóng giao tiếp SPI.

#### **Ví dụ:**
```cpp
#include <SPI.h>

void setup() {
  Serial.begin(9600);
  SPI.begin();
  byte receivedData = SPI.transfer(0xFF); // Gửi dữ liệu 0xFF và nhận phản hồi
  Serial.println(receivedData, HEX); // In dữ liệu nhận được dưới dạng hex
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Giao tiếp đồng bộ, dùng cho việc trao đổi dữ liệu tốc độ cao với các thiết bị ngoại vi như cảm biến, bộ nhớ.

---

### **2. Print**

#### **Mô tả:**
- **`Print`** là một lớp (class) cơ bản cho phép bạn gửi dữ liệu (chuỗi hoặc số) đến các thiết bị đầu ra như màn hình LCD, Serial Monitor, v.v.
- Các hàm như `print()`, `println()` được kế thừa từ lớp **`Print`**.

#### **Cú pháp cơ bản:**
```cpp
Serial.print(data);   // In dữ liệu mà không xuống dòng
Serial.println(data); // In dữ liệu và xuống dòng
```

- **`print()`**: In dữ liệu mà không xuống dòng.
- **`println()`**: In dữ liệu và xuống dòng.

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
  Serial.print("Hello, ");
  Serial.println("World!");
}

void loop() {
  // In ra "Hello, World!" và xuống dòng
}
```

#### **Chức năng:**
- Gửi dữ liệu tới màn hình hoặc Serial Monitor, thường dùng để debug hoặc hiển thị thông tin.

---

### **3. Serial**

#### **Mô tả:**
- **`Serial`** là một giao thức giao tiếp nối tiếp giữa Arduino và máy tính. Nó cho phép truyền tải dữ liệu thông qua cổng USB, thường dùng để đọc và ghi dữ liệu trong quá trình phát triển.
- Các hàm như `Serial.begin()`, `Serial.print()`, `Serial.read()` được sử dụng để giao tiếp qua cổng nối tiếp.

#### **Cú pháp cơ bản:**
```cpp
Serial.begin(baudRate);  // Khởi tạo Serial với tốc độ truyền
Serial.print(data);      // In dữ liệu
Serial.read();           // Đọc dữ liệu từ Serial
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);    // Khởi tạo giao tiếp Serial với tốc độ 9600
  Serial.println("Hello, Arduino!");
}

void loop() {
  // Đọc và in dữ liệu từ Serial
  if (Serial.available()) {
    char incomingData = Serial.read();
    Serial.print("Received: ");
    Serial.println(incomingData);
  }
}
```

#### **Chức năng:**
- Giao tiếp nối tiếp với máy tính hoặc các thiết bị khác qua cổng USB.

---

### **4. Stream**

#### **Mô tả:**
- **`Stream`** là một lớp cơ bản trong Arduino, kế thừa bởi các lớp như `Serial`, `Ethernet`, `WiFi`, và `File`. Nó cho phép xử lý luồng dữ liệu (streaming) một cách dễ dàng.
- Các hàm như `available()`, `read()`, `write()` là các phương thức của lớp `Stream`.

#### **Cú pháp cơ bản:**
```cpp
Stream.read();    // Đọc 1 byte dữ liệu
Stream.write(data); // Gửi 1 byte dữ liệu
Stream.available(); // Kiểm tra xem có dữ liệu để đọc không
```

#### **Ví dụ:**
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) {
    char data = Serial.read();
    Serial.write(data); // Gửi lại dữ liệu nhận được
  }
}
```

#### **Chức năng:**
- Xử lý luồng dữ liệu giữa các thiết bị, như đọc và ghi dữ liệu nối tiếp hoặc qua các giao thức mạng.

---

### **5. Wire (I2C Communication)**

#### **Mô tả:**
- **`Wire`** là thư viện để giao tiếp I2C giữa Arduino và các thiết bị ngoại vi như cảm biến hoặc màn hình. I2C sử dụng hai dây: **SDA (Serial Data)** và **SCL (Serial Clock)**.

#### **Cú pháp cơ bản:**
```cpp
#include <Wire.h>

Wire.begin();            // Khởi tạo giao tiếp I2C
Wire.requestFrom(address, numBytes);  // Yêu cầu dữ liệu từ thiết bị ngoại vi
Wire.beginTransmission(address);  // Bắt đầu truyền dữ liệu đến thiết bị
Wire.write(data);        // Gửi dữ liệu
Wire.endTransmission();  // Kết thúc truyền
```

#### **Ví dụ:**
```cpp
#include <Wire.h>

void setup() {
  Serial.begin(9600);
  Wire.begin();               // Khởi tạo giao tiếp I2C
  Wire.beginTransmission(0x3C); // Địa chỉ của thiết bị I2C
  Wire.write(0x01);           // Gửi dữ liệu
  Wire.endTransmission();     // Kết thúc truyền
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Giao tiếp I2C với các thiết bị ngoại vi sử dụng hai dây (SDA và SCL).

---

### **Tóm tắt và Ứng dụng**

| **Giao thức/Thư viện** | **Mô tả**                                              | **Ví dụ sử dụng**                                        |
|------------------------|--------------------------------------------------------|----------------------------------------------------------|
| **SPI**                | Giao thức đồng bộ cho truyền thông tốc độ cao giữa vi điều khiển và thiết bị ngoại vi. | Giao tiếp với cảm biến hoặc bộ nhớ qua SPI.              |
| **Print**              | In dữ liệu tới màn hình hoặc Serial Monitor.            | In dữ liệu ra Serial Monitor để debug hoặc hiển thị thông tin. |
| **Serial**             | Giao tiếp nối tiếp qua cổng USB giữa Arduino và máy tính. | Gửi và nhận dữ liệu qua cổng USB cho mục đích debug hoặc truyền thông. |
| **Stream**             | Xử lý luồng dữ liệu, kế thừa bởi nhiều thư viện giao tiếp. | Đọc và ghi dữ liệu nối tiếp trong các giao thức như Serial, Ethernet, WiFi. |
| **Wire**               | Giao tiếp I2C để kết nối với các thiết bị ngoại vi.    | Giao tiếp với các cảm biến hoặc màn hình qua I2C.         |

#### **Ứng dụng thực tế**:
1. **Giao tiếp tốc độ cao**: Dùng SPI để giao tiếp nhanh chóng với các thiết bị ngoại vi như cảm biến, bộ nhớ.
2. **Truyền thông nối tiếp**: Dùng Serial và Print để debug chương trình hoặc gửi thông tin đến máy tính.
3. **Giao tiếp I2C**: Sử dụng Wire để giao tiếp với nhiều thiết bị ngoại vi qua một cặp dây SDA và SCL, tiết kiệm chân.

# USB
### **USB, Keyboard, and Mouse in Arduino**

Arduino can interface with USB devices like keyboards and mice using specific libraries, enabling it to interact with these devices or emulate them. Below is an overview of how these functionalities work in Arduino:

---

### **1. USB in Arduino**

#### **Mô tả:**
- **USB** trên Arduino chủ yếu liên quan đến giao tiếp nối tiếp (Serial Communication) thông qua cổng USB của board Arduino để giao tiếp với máy tính.
- Arduino sử dụng cổng USB để lập trình và truyền dữ liệu, đồng thời cũng có thể giao tiếp với các thiết bị USB khác như bàn phím, chuột, và các thiết bị ngoại vi khác nếu board hỗ trợ.

#### **Ứng dụng:**
- Gửi và nhận dữ liệu giữa Arduino và máy tính.
- Cung cấp nguồn năng lượng cho board Arduino từ máy tính qua cổng USB.
- Có thể mô phỏng thiết bị USB (như bàn phím và chuột) nếu sử dụng các board hỗ trợ như **Arduino Leonardo**, **Arduino Micro**, hoặc **Arduino Due**, vì chúng có khả năng hoạt động như thiết bị USB trực tiếp.

---

### **2. Keyboard (Bàn phím)**

#### **Mô tả:**
- Arduino có thể mô phỏng một bàn phím USB để gửi phím bấm đến máy tính. Điều này có thể được thực hiện bằng cách sử dụng thư viện **Keyboard**.
- Thư viện này chỉ hoạt động trên các board như **Arduino Leonardo**, **Arduino Micro**, hoặc **Arduino Due**, vì chúng hỗ trợ giao tiếp USB natively.

#### **Cú pháp cơ bản:**
```cpp
#include <Keyboard.h>

void setup() {
  // Khởi tạo giao tiếp với bàn phím
  Keyboard.begin();
  delay(1000); // Chờ một chút
  Keyboard.print("Hello, World!"); // Gửi chuỗi văn bản đến máy tính
  delay(1000);
  Keyboard.end(); // Kết thúc giao tiếp với bàn phím
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Gửi các ký tự hoặc tổ hợp phím tới máy tính.
- Mô phỏng các phím bấm như **Ctrl**, **Alt**, **Shift**, và các phím chữ, số.
- Có thể tạo các phím tắt tự động cho các tác vụ.

#### **Ví dụ ứng dụng:**
- Mở các chương trình hoặc thực hiện các thao tác tự động trên máy tính (ví dụ: mở trình duyệt, gõ văn bản tự động).

---

### **3. Mouse (Chuột)**

#### **Mô tả:**
- **Thư viện Mouse** cho phép Arduino mô phỏng các hoạt động của chuột USB, ví dụ như di chuyển con trỏ, nhấn chuột, hoặc cuộn chuột.
- Tương tự như thư viện **Keyboard**, thư viện **Mouse** cũng chỉ hoạt động trên các board hỗ trợ giao tiếp USB, như **Arduino Leonardo**, **Arduino Micro**, và **Arduino Due**.

#### **Cú pháp cơ bản:**
```cpp
#include <Mouse.h>

void setup() {
  // Khởi tạo giao tiếp với chuột
  Mouse.begin();
  delay(1000);  // Chờ một chút
  Mouse.move(50, 0); // Di chuyển con trỏ chuột 50 đơn vị sang phải
  Mouse.click(MOUSE_LEFT); // Nhấn chuột trái
  delay(1000);
  Mouse.end(); // Kết thúc giao tiếp với chuột
}

void loop() {
  // Không có hành động gì trong loop
}
```

#### **Chức năng:**
- Di chuyển con trỏ chuột trên màn hình.
- Nhấn các nút chuột như trái, phải, hoặc giữa.
- Thực hiện cuộn chuột hoặc kéo thả chuột.
- Điều khiển chuột qua phần cứng thay vì sử dụng thiết bị ngoại vi.

#### **Ví dụ ứng dụng:**
- Điều khiển máy tính từ xa, tạo chuột ảo cho các dự án điều khiển tự động.
- Tạo các chương trình hoặc trò chơi điều khiển bằng chuột.

---

### **Tóm tắt và Ứng dụng**

| **Chức năng**           | **Mô tả**                                               | **Ứng dụng**                                                        |
|-------------------------|---------------------------------------------------------|--------------------------------------------------------------------|
| **USB**                 | Giao tiếp nối tiếp qua cổng USB, truyền tải dữ liệu và cung cấp năng lượng. | Giao tiếp giữa Arduino và máy tính, cấp nguồn cho board Arduino.  |
| **Keyboard**            | Mô phỏng bàn phím USB để gửi phím bấm đến máy tính.     | Tự động gõ văn bản, tạo phím tắt, điều khiển máy tính qua bàn phím.|
| **Mouse**               | Mô phỏng chuột USB để di chuyển và nhấn chuột.          | Điều khiển máy tính từ xa, tạo chuột ảo cho các dự án điều khiển tự động. |

### **Ứng dụng thực tế:**
1. **Mô phỏng bàn phím**: Tạo các ứng dụng tự động gửi văn bản hoặc thao tác phím vào các phần mềm trên máy tính.
2. **Điều khiển chuột**: Tạo các công cụ tự động điều khiển chuột hoặc xây dựng các dự án nhập liệu tự động từ Arduino.
3. **Giao tiếp USB**: Arduino sử dụng USB để truyền tải dữ liệu hoặc cấp nguồn, rất tiện lợi cho các dự án cần giao tiếp giữa Arduino và máy tính.

---

Với các thư viện **Keyboard** và **Mouse**, Arduino có thể trở thành công cụ rất mạnh mẽ trong việc mô phỏng các thiết bị ngoại vi USB, mở ra khả năng sáng tạo vô hạn cho các dự án tự động hóa và giao tiếp.

# Wi-Fi

### **Wi-Fi trong Arduino**

Arduino có nhiều thư viện và module cho phép bạn kết nối bo mạch Arduino với mạng Wi-Fi, giao tiếp qua internet và tương tác với các thiết bị khác qua kết nối không dây. Thư viện phổ biến nhất để sử dụng Wi-Fi trong Arduino là thư viện **WiFi**, hoạt động với các bo mạch như **Arduino Uno WiFi**, **ESP8266** và **ESP32**. Dưới đây là các thành phần chính của chức năng Wi-Fi trong Arduino.

---

### **1. Tổng quan về Wi-Fi**

#### **Mô tả:**
- Chức năng Wi-Fi trong Arduino cho phép bạn kết nối bo mạch Arduino với mạng không dây (Wi-Fi) và giao tiếp với các thiết bị khác qua internet.
- Điều này rất hữu ích cho các dự án Internet of Things (IoT), nơi Arduino cần gửi dữ liệu đến các dịch vụ đám mây hoặc giao tiếp với các thiết bị khác qua internet.

#### **Ứng dụng:**
- Kết nối với các nền tảng đám mây như **ThingSpeak**, **Blynk**, hoặc **Adafruit IO**.
- Gửi dữ liệu cảm biến qua internet.
- Giao tiếp giữa nhiều thiết bị hoặc máy chủ qua Wi-Fi.

---

### **2. Mạng Wi-Fi**

#### **Mô tả:**
- Thư viện `WiFi` cho phép Arduino kết nối với mạng Wi-Fi. Bạn cần cung cấp **SSID** (tên mạng) và **mật khẩu** để thiết lập kết nối.
- Chức năng này hoạt động với các bo mạch có khả năng kết nối Wi-Fi như **ESP8266**, **ESP32** hoặc **Arduino Uno WiFi**.

#### **Ví dụ:**
```cpp
#include <WiFi.h>  // Cho ESP32 hoặc ESP8266

const char* ssid = "your-SSID";  // Tên mạng Wi-Fi
const char* password = "your-PASSWORD";  // Mật khẩu Wi-Fi

void setup() {
  Serial.begin(115200);
  
  // Kết nối Wi-Fi
  WiFi.begin(ssid, password);
  
  // Chờ kết nối
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Đang kết nối Wi-Fi...");
  }
  Serial.println("Kết nối thành công Wi-Fi!");
}

void loop() {
  // Wi-Fi đã kết nối, thực hiện các tác vụ khác ở đây
}
```

#### **Chức năng:**
- **`WiFi.begin()`**: Kết nối Arduino với mạng Wi-Fi với SSID và mật khẩu đã chỉ định.
- **`WiFi.status()`**: Kiểm tra trạng thái hiện tại của kết nối Wi-Fi.
- **`WL_CONNECTED`**: Hằng số chỉ ra kết nối thành công.

---

### **3. IPAddress**

#### **Mô tả:**
- Lớp `IPAddress` trong Arduino được sử dụng để đại diện và làm việc với địa chỉ IP. Nó thường được sử dụng khi kết nối Arduino với mạng Wi-Fi hoặc khi làm việc với các thiết bị mạng.
- Lớp này rất hữu ích khi gán IP tĩnh hoặc kiểm tra địa chỉ IP của bo mạch sau khi nó kết nối với mạng Wi-Fi.

#### **Ví dụ:**
```cpp
#include <WiFi.h>

const char* ssid = "your-SSID";
const char* password = "your-PASSWORD";

void setup() {
  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
  Serial.println("Kết nối Wi-Fi thành công");
  
  // In địa chỉ IP của Arduino
  Serial.println(WiFi.localIP());
}

void loop() {
  // Thực hiện các tác vụ khác
}
```

#### **Chức năng:**
- **`WiFi.localIP()`**: Trả về địa chỉ IP cục bộ được gán cho Arduino sau khi nó kết nối với mạng Wi-Fi.
- **`IPAddress`**: Lớp đại diện và quản lý địa chỉ IP.

---

### **4. WiFiClient**

#### **Mô tả:**
- `WiFiClient` được sử dụng để tạo kết nối client đến một máy chủ từ xa qua mạng Wi-Fi.
- Nó thường được sử dụng để gửi hoặc nhận dữ liệu qua các yêu cầu HTTP hoặc giao tiếp với các thiết bị khác trên cùng mạng.

#### **Ví dụ:**
```cpp
#include <WiFi.h>

const char* ssid = "your-SSID";
const char* password = "your-PASSWORD";
const char* host = "example.com";  // Máy chủ từ xa

WiFiClient client;

void setup() {
  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
  Serial.println("Kết nối Wi-Fi thành công");

  if (client.connect(host, 80)) {
    client.println("GET / HTTP/1.1");
    client.println("Host: example.com");
    client.println("Connection: close");
    client.println();
  }
}

void loop() {
  if (client.available()) {
    String line = client.readStringUntil('\n');
    Serial.println(line);
  }
}
```

#### **Chức năng:**
- **`WiFiClient.connect()`**: Thiết lập kết nối đến máy chủ từ xa.
- **`client.println()`**: Gửi yêu cầu đến máy chủ.
- **`client.available()`**: Kiểm tra xem có dữ liệu có sẵn để đọc từ máy chủ không.

---

### **5. WiFiServer**

#### **Mô tả:**
- `WiFiServer` được sử dụng để tạo một máy chủ lắng nghe các kết nối client đến qua mạng Wi-Fi.
- Nó có thể xử lý nhiều kết nối client, rất hữu ích cho các dự án IoT như máy chủ web, hoặc điều khiển Arduino qua Wi-Fi.

#### **Ví dụ:**
```cpp
#include <WiFi.h>

const char* ssid = "your-SSID";
const char* password = "your-PASSWORD";

WiFiServer server(80);  // Tạo máy chủ trên cổng 80 (HTTP)

void setup() {
  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
  Serial.println("Kết nối Wi-Fi thành công");
  server.begin();  // Bắt đầu máy chủ
}

void loop() {
  WiFiClient client = server.available();  // Lắng nghe các client đến
  
  if (client) {
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        Serial.write(c);
        client.write(c);  // Phản hồi lại ký tự nhận được cho client
      }
    }
    client.stop();
  }
}
```

#### **Chức năng:**
- **`server.begin()`**: Bắt đầu máy chủ trên cổng đã chỉ định.
- **`server.available()`**: Kiểm tra các kết nối client đến.
- **`client.write()`**: Gửi dữ liệu trả lại cho client.

---

### **6. WiFiUDP**

#### **Mô tả:**
- `WiFiUDP` được sử dụng để gửi và nhận dữ liệu qua **UDP (User Datagram Protocol)** trên mạng Wi-Fi.
- Khác với TCP, UDP là giao thức không kết nối, khiến nó nhanh hơn nhưng ít tin cậy hơn.

#### **Ví dụ:**
```cpp
#include <WiFi.h>
#include <WiFiUdp.h>

const char* ssid = "your-SSID";
const char* password = "your-PASSWORD";

WiFiUDP Udp;
unsigned int localPort = 4210;  // Cổng local để lắng nghe gói UDP

void setup() {
  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
  Serial.println("Kết nối Wi-Fi thành công");
  
  Udp.begin(localPort);  // Bắt đầu lắng nghe trên cổng local
}

void loop() {
  int packetSize = Udp.parsePacket();
  if (packetSize) {
    char incomingPacket[255];
    Udp.read(incomingPacket, packetSize);
    Serial.println("Nhận gói UDP:");
    Serial.println(incomingPacket);
  }
}
```

#### **Chức năng:**
- **`Udp.begin()`**: Khởi tạo giao tiếp UDP trên cổng đã chỉ định.
- **`Udp.parsePacket()`**: Kiểm tra xem có gói UDP nào đến không.
- **`Udp.read()`**: Đọc gói UDP nhận được.

---

### **Tóm tắt và Ứng dụng**

| **Thành phần**         | **Mô tả**                                                       | **Ứng dụng**                                                           |
|------------------------|---------------------------------------------------------------|-----------------------------------------------------------------------|
| **WiFi Network**        | Kết nối Arduino với mạng Wi-Fi.                               | Các ứng dụng Internet of Things (IoT), kết nối đám mây.               |
| **IPAddress**           | Đại diện và làm việc với địa chỉ IP.                         | Gán IP tĩnh, in địa chỉ IP sau khi kết nối Wi-Fi.                      |
| **WiFiClient**          | Tạo kết nối client đến máy chủ từ xa qua Wi-Fi

.               | Gửi dữ liệu qua các yêu cầu HTTP, giao tiếp với các máy chủ.          |
| **WiFiServer**          | Tạo máy chủ Wi-Fi nhận kết nối từ các client.                 | Điều khiển từ xa, tạo máy chủ web.                                    |
| **WiFiUDP**             | Gửi và nhận dữ liệu qua UDP.                                  | Các ứng dụng không yêu cầu kết nối liên tục, giao tiếp nhanh.         |

**Ứng dụng thực tế** của các tính năng này bao gồm điều khiển thiết bị từ xa, thu thập và gửi dữ liệu cảm biến, giao tiếp với các dịch vụ đám mây, và xây dựng các hệ thống IoT kết nối qua Wi-Fi.

---


# Sketch

Trong Arduino, **Sketch** là chương trình bạn viết để điều khiển các thiết bị phần cứng. Mỗi sketch bao gồm hai hàm chính: **setup()** và **loop()**. Dưới đây là mô tả chi tiết về chúng:

### 1. **Sketch**
   - **Định nghĩa**: "Sketch" trong Arduino là tên gọi cho một chương trình hoặc mã nguồn mà bạn viết để điều khiển các thiết bị phần cứng của Arduino. Các sketch được biên dịch và tải lên board Arduino thông qua phần mềm Arduino IDE.
   - **Cấu trúc**: Mỗi sketch sẽ có ít nhất hai hàm chính là `setup()` và `loop()`.

### 2. **Hàm setup()**
   - **Mô tả**: Hàm `setup()` được gọi một lần khi board Arduino bắt đầu chạy, hoặc khi board được reset. Đây là nơi bạn sẽ đặt các lệnh khởi tạo hoặc cấu hình các thiết bị và biến trước khi chương trình bắt đầu hoạt động.
   - **Chức năng**: 
     - Cấu hình các chân I/O (như `pinMode()`)
     - Khởi tạo các giao thức (như `Serial.begin()`)
     - Các bước chuẩn bị khác như bật/tắt thiết bị.
   - **Ví dụ**:

```cpp
void setup() {
  // Khởi tạo serial communication với tốc độ 9600 bps
  Serial.begin(9600);
  
  // Cấu hình chân 13 là OUTPUT để điều khiển đèn LED
  pinMode(13, OUTPUT);
}
```

**Giải thích**:
   - `Serial.begin(9600);`: Khởi tạo giao tiếp Serial với tốc độ truyền dữ liệu là 9600 baud.
   - `pinMode(13, OUTPUT);`: Cấu hình chân 13 của Arduino là chân output để điều khiển một thiết bị (ví dụ như đèn LED).

### 3. **Hàm loop()**
   - **Mô tả**: Sau khi `setup()` hoàn tất, chương trình sẽ chuyển sang hàm `loop()`. Hàm `loop()` sẽ chạy liên tục và lặp đi lặp lại trong suốt quá trình board Arduino hoạt động. Đây là nơi bạn đặt mã điều khiển thực tế, mà board Arduino sẽ thực thi liên tục trong suốt thời gian chạy.
   - **Chức năng**: 
     - Điều khiển thiết bị trong thời gian thực.
     - Xử lý dữ liệu cảm biến hoặc các tác vụ lặp đi lặp lại.
     - Đảm bảo hệ thống hoạt động liên tục.
   - **Ví dụ**:

```cpp
void loop() {
  // Bật đèn LED trên chân 13
  digitalWrite(13, HIGH);
  
  // Đợi 1 giây
  delay(1000);
  
  // Tắt đèn LED trên chân 13
  digitalWrite(13, LOW);
  
  // Đợi 1 giây
  delay(1000);
}
```

**Giải thích**:
   - `digitalWrite(13, HIGH);`: Bật đèn LED trên chân 13.
   - `delay(1000);`: Dừng chương trình trong 1000 mili-giây (1 giây).
   - `digitalWrite(13, LOW);`: Tắt đèn LED trên chân 13.
   - Quá trình này sẽ tiếp tục lặp đi lặp lại vì hàm `loop()` không bao giờ dừng lại.

### Tóm tắt:
| Hàm      | Mô tả                                              | Ví dụ                                                                 |
|----------|----------------------------------------------------|-----------------------------------------------------------------------|
| `setup()` | Chạy 1 lần khi bắt đầu hoặc khi reset board Arduino. Dùng để cấu hình các chân, thiết lập giao tiếp, khởi tạo biến. | `Serial.begin(9600);`, `pinMode(13, OUTPUT);`                        |
| `loop()`  | Chạy liên tục sau khi `setup()` hoàn thành. Dùng để thực hiện các tác vụ lặp đi lặp lại. | `digitalWrite(13, HIGH);`, `delay(1000);`, `digitalWrite(13, LOW);` |

Các hàm này tạo thành cấu trúc cơ bản của mỗi sketch trong Arduino. Bạn sẽ sử dụng chúng để khởi tạo các thiết bị và xử lý các tác vụ điều khiển trong một vòng lặp liên tục.

# Arithmetic Operators

Trong Arduino, **Arithmetic Operators** (Toán tử số học) được sử dụng để thực hiện các phép toán cơ bản trên các giá trị số. Dưới đây là mô tả và ví dụ cho các toán tử số học trong Arduino:

### 1. **+ (Addition) - Phép cộng**
   - **Mô tả**: Thực hiện phép cộng giữa hai toán hạng.
   - **Cú pháp**: 
     ```cpp
     result = a + b;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 5;
     int b = 3;
     int result = a + b;  // result = 8
     ```

### 2. **= (Assignment Operator) - Toán tử gán**
   - **Mô tả**: Gán giá trị của biểu thức bên phải cho biến bên trái.
   - **Cú pháp**: 
     ```cpp
     variable = value;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 10;  // Gán giá trị 10 cho biến a
     ```

### 3. **/ (Division) - Phép chia**
   - **Mô tả**: Thực hiện phép chia giữa hai toán hạng.
   - **Cú pháp**: 
     ```cpp
     result = a / b;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 10;
     int b = 2;
     int result = a / b;  // result = 5
     ```

### 4. **\* (Multiplication) - Phép nhân**
   - **Mô tả**: Thực hiện phép nhân giữa hai toán hạng.
   - **Cú pháp**: 
     ```cpp
     result = a * b;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 4;
     int b = 3;
     int result = a * b;  // result = 12
     ```

### 5. **% (Remainder) - Phép lấy dư**
   - **Mô tả**: Trả về phần dư của phép chia giữa hai toán hạng.
   - **Cú pháp**: 
     ```cpp
     result = a % b;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 10;
     int b = 3;
     int result = a % b;  // result = 1 (vì 10 chia cho 3 dư 1)
     ```

### 6. **- (Subtraction) - Phép trừ**
   - **Mô tả**: Thực hiện phép trừ giữa hai toán hạng.
   - **Cú pháp**: 
     ```cpp
     result = a - b;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 8;
     int b = 3;
     int result = a - b;  // result = 5
     ```

### Tóm tắt:

| Toán tử | Tên gọi            | Mô tả                                        | Ví dụ                        |
|---------|--------------------|----------------------------------------------|------------------------------|
| `+`     | Cộng               | Cộng hai toán hạng                           | `result = a + b;`            |
| `=`     | Gán                | Gán giá trị của biểu thức cho biến           | `a = 10;`                    |
| `/`     | Chia               | Chia hai toán hạng                           | `result = a / b;`            |
| `*`     | Nhân               | Nhân hai toán hạng                           | `result = a * b;`            |
| `%`     | Lấy dư             | Lấy phần dư của phép chia                    | `result = a % b;`            |
| `-`     | Trừ                | Trừ hai toán hạng                            | `result = a - b;`            |

Các toán tử số học này là các phép toán cơ bản trong lập trình Arduino, được sử dụng để tính toán và xử lý dữ liệu số trong các dự án của bạn.

# Pointer Access Operators

Trong Arduino, **Pointer Access Operators** (Toán tử truy cập con trỏ) được sử dụng để làm việc với con trỏ và tham chiếu. Có hai toán tử chính trong C++ (ngôn ngữ sử dụng trong Arduino) liên quan đến con trỏ: **`*` (dereference operator)** và **`&` (reference operator)**. Dưới đây là mô tả chi tiết về chúng:

### 1. **`*` (Dereference Operator) - Toán tử giải tham chiếu**
   - **Mô tả**: Toán tử `*` được sử dụng để truy cập giá trị mà con trỏ đang trỏ tới. Nó giúp giải tham chiếu (dereference) con trỏ để lấy giá trị thực tế mà con trỏ đó lưu trữ.
   - **Cú pháp**: 
     ```cpp
     value = *pointer;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 10;
     int* ptr = &a;  // Con trỏ ptr lưu địa chỉ của biến a
     
     // Sử dụng toán tử * để truy cập giá trị mà ptr đang trỏ tới
     int b = *ptr;  // b = 10
     ```

   **Giải thích**:
   - `int a = 10;`: Khai báo biến `a` có giá trị là 10.
   - `int* ptr = &a;`: Khai báo con trỏ `ptr` và gán cho nó địa chỉ của biến `a`.
   - `int b = *ptr;`: Sử dụng toán tử `*` để giải tham chiếu và lấy giá trị mà `ptr` đang trỏ tới, đó chính là giá trị của `a`, tức là `10`.

### 2. **`&` (Reference Operator) - Toán tử tham chiếu**
   - **Mô tả**: Toán tử `&` được sử dụng để lấy địa chỉ của một biến, tức là nó trả về địa chỉ bộ nhớ của biến thay vì giá trị của nó. Đây là cách để tạo con trỏ, vì bạn cần biết địa chỉ của biến để con trỏ có thể trỏ tới.
   - **Cú pháp**: 
     ```cpp
     pointer = &variable;
     ```
   - **Ví dụ**:
     ```cpp
     int a = 10;
     int* ptr = &a;  // Lấy địa chỉ của a và gán cho ptr
     ```

   **Giải thích**:
   - `int a = 10;`: Khai báo biến `a` có giá trị là 10.
   - `int* ptr = &a;`: Lấy địa chỉ của biến `a` bằng toán tử `&` và gán nó cho con trỏ `ptr`.

### Tóm tắt:

| Toán tử | Tên gọi              | Mô tả                                          | Ví dụ                              |
|---------|----------------------|------------------------------------------------|------------------------------------|
| `*`     | Toán tử giải tham chiếu | Truy cập giá trị mà con trỏ đang trỏ tới.      | `int b = *ptr;`                   |
| `&`     | Toán tử tham chiếu    | Lấy địa chỉ của một biến.                     | `ptr = &a;`                       |

### Ví dụ kết hợp cả hai toán tử:

```cpp
int a = 5;
int* ptr = &a;  // Lấy địa chỉ của a và gán cho con trỏ ptr

// Sử dụng * để truy cập giá trị mà ptr đang trỏ tới và thay đổi giá trị của a
*ptr = 10;  // Thay đổi giá trị của a thông qua ptr

Serial.println(a);  // In ra 10, vì giá trị của a đã được thay đổi qua ptr
```

**Giải thích**:
- `int* ptr = &a;`: Lấy địa chỉ của `a` và gán cho con trỏ `ptr`.
- `*ptr = 10;`: Thông qua con trỏ `ptr`, bạn thay đổi giá trị của `a` thành 10.
- Kết quả là giá trị của `a` sẽ là 10 khi in ra màn hình.

Các toán tử này là phần quan trọng trong việc làm việc với con trỏ và tham chiếu trong C++ và Arduino, cho phép bạn thao tác với bộ nhớ một cách hiệu quả.

# Control Structure

Trong Arduino (và C/C++ nói chung), **Control Structures** (Cấu trúc điều khiển) là các câu lệnh cho phép bạn điều khiển luồng thực thi của chương trình. Dưới đây là mô tả và ví dụ cho các cấu trúc điều khiển phổ biến:

### 1. **`break`**
   - **Mô tả**: Dùng để thoát ra khỏi một vòng lặp hoặc câu lệnh `switch`. Khi `break` được gặp, vòng lặp hoặc câu lệnh `switch` sẽ kết thúc ngay lập tức.
   - **Cú pháp**: 
     ```cpp
     break;
     ```
   - **Ví dụ**:
     ```cpp
     for (int i = 0; i < 10; i++) {
       if (i == 5) {
         break;  // Thoát khỏi vòng lặp khi i bằng 5
       }
     }
     ```

### 2. **`continue`**
   - **Mô tả**: Dùng để bỏ qua phần còn lại của một vòng lặp hiện tại và chuyển đến vòng lặp tiếp theo. `continue` chỉ có tác dụng trong các vòng lặp như `for`, `while`, và `do...while`.
   - **Cú pháp**: 
     ```cpp
     continue;
     ```
   - **Ví dụ**:
     ```cpp
     for (int i = 0; i < 10; i++) {
       if (i == 5) {
         continue;  // Bỏ qua khi i bằng 5, vòng lặp sẽ tiếp tục
       }
     }
     ```

### 3. **`do...while`**
   - **Mô tả**: Đây là một vòng lặp kiểm tra điều kiện sau khi thực hiện mã ít nhất một lần. Điều kiện được kiểm tra sau khi mỗi vòng lặp.
   - **Cú pháp**: 
     ```cpp
     do {
       // Thực hiện các câu lệnh
     } while (condition);
     ```
   - **Ví dụ**:
     ```cpp
     int i = 0;
     do {
       i++;
     } while (i < 5);  // Vòng lặp sẽ thực hiện ít nhất một lần
     ```

### 4. **`else`**
   - **Mô tả**: Được sử dụng kết hợp với câu lệnh `if` để chỉ định một khối mã được thực thi nếu điều kiện trong `if` không đúng.
   - **Cú pháp**: 
     ```cpp
     if (condition) {
       // Thực hiện khi điều kiện đúng
     } else {
       // Thực hiện khi điều kiện sai
     }
     ```
   - **Ví dụ**:
     ```cpp
     int a = 5;
     if (a > 10) {
       // Không thực thi
     } else {
       // Thực thi vì a không lớn hơn 10
     }
     ```

### 5. **`for`**
   - **Mô tả**: Là vòng lặp lặp lại một số lần nhất định. Cấu trúc của vòng lặp `for` bao gồm ba phần: khởi tạo, điều kiện kiểm tra, và thay đổi biến lặp lại.
   - **Cú pháp**: 
     ```cpp
     for (initialization; condition; increment) {
       // Thực hiện mã khi điều kiện đúng
     }
     ```
   - **Ví dụ**:
     ```cpp
     for (int i = 0; i < 10; i++) {
       // Thực hiện mã cho i từ 0 đến 9
     }
     ```

### 6. **`goto`**
   - **Mô tả**: Dùng để nhảy đến một nhãn trong chương trình. Mặc dù có thể sử dụng, nhưng `goto` thường bị tránh vì nó làm cho mã trở nên khó hiểu và khó bảo trì.
   - **Cú pháp**: 
     ```cpp
     goto label;
     ```
   - **Ví dụ**:
     ```cpp
     int i = 0;
     start:
     i++;
     if (i < 5) goto start;  // Lặp lại cho đến khi i >= 5
     ```

### 7. **`if`**
   - **Mô tả**: Câu lệnh điều kiện kiểm tra một điều kiện và thực thi mã nếu điều kiện đó đúng.
   - **Cú pháp**: 
     ```cpp
     if (condition) {
       // Thực hiện khi điều kiện đúng
     }
     ```
   - **Ví dụ**:
     ```cpp
     int a = 5;
     if (a > 3) {
       // Thực hiện vì a lớn hơn 3
     }
     ```

### 8. **`return`**
   - **Mô tả**: Dùng để trả giá trị từ một hàm và kết thúc thực thi của hàm đó. Nếu hàm không trả giá trị, chỉ cần dùng `return` mà không cần giá trị.
   - **Cú pháp**: 
     ```cpp
     return value; // Trả về giá trị và kết thúc hàm
     ```
   - **Ví dụ**:
     ```cpp
     int add(int a, int b) {
       return a + b;  // Trả về tổng của a và b
     }
     ```

### 9. **`switch...case`**
   - **Mô tả**: Câu lệnh `switch` kiểm tra một giá trị đối chiếu với các giá trị `case` khác nhau và thực thi khối mã tương ứng. Nếu không có giá trị nào khớp, câu lệnh `default` sẽ được thực thi.
   - **Cú pháp**: 
     ```cpp
     switch (expression) {
       case value1:
         // Thực hiện nếu expression == value1
         break;
       case value2:
         // Thực hiện nếu expression == value2
         break;
       default:
         // Thực hiện nếu không có giá trị nào khớp
     }
     ```
   - **Ví dụ**:
     ```cpp
     int x = 2;
     switch (x) {
       case 1:
         // Không thực thi
         break;
       case 2:
         // Thực thi
         break;
       default:
         // Không thực thi
     }
     ```

### 10. **`while`**
   - **Mô tả**: Vòng lặp `while` thực thi một khối mã trong khi điều kiện là đúng. Kiểm tra điều kiện trước mỗi lần thực hiện vòng lặp.
   - **Cú pháp**: 
     ```cpp
     while (condition) {
       // Thực hiện khi điều kiện đúng
     }
     ```
   - **Ví dụ**:
     ```cpp
     int i = 0;
     while (i < 5) {
       i++;  // Lặp lại khi i < 5
     }
     ```

### Tóm tắt các cấu trúc điều khiển trong Arduino:

| Cấu trúc       | Mô tả                                      | Ví dụ                               |
|----------------|--------------------------------------------|-------------------------------------|
| `break`        | Thoát khỏi vòng lặp hoặc `switch`         | `break;`                            |
| `continue`     | Bỏ qua vòng lặp hiện tại, tiếp tục vòng lặp tiếp theo | `continue;`                         |
| `do...while`   | Vòng lặp kiểm tra điều kiện sau mỗi lần lặp | `do { ... } while (condition);`     |
| `else`         | Thực thi nếu điều kiện `if` sai           | `else { ... }`                      |
| `for`          | Vòng lặp xác định số lần thực hiện        | `for (int i = 0; i < 10; i++) { ... }` |
| `goto`         | Nhảy đến một nhãn trong chương trình      | `goto label;`                       |
| `if`           | Kiểm tra điều kiện                        | `if (condition) { ... }`            |
| `return`       | Trả về giá trị từ một hàm                 | `return value;`                     |
| `switch...case`| Kiểm tra giá trị với các case khác nhau   | `switch (x) { case 1: ... }`        |
| `while`        | Vòng lặp kiểm tra điều kiện trước khi thực hiện | `while (condition) { ... }`        |

Những cấu trúc điều khiển này giúp bạn quản lý luồng thực thi trong chương trình Arduino của mình, từ việc lặp lại công việc đến việc điều khiển theo các điều kiện khác nhau.

# Comparison Operators

Trong Arduino (và C/C++ nói chung), **Comparison Operators** (Toán tử so sánh) được sử dụng để so sánh hai giá trị và trả về một giá trị boolean (`true` hoặc `false`) tùy vào kết quả của phép so sánh đó. Dưới đây là mô tả và ví dụ cho các toán tử so sánh phổ biến:

### 1. **`==` (Equal to - Bằng)**
   - **Mô tả**: So sánh hai giá trị, nếu chúng bằng nhau thì trả về `true`, nếu không thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 == value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 5;
     if (x == 5) {
       // Điều kiện đúng vì x bằng 5
     }
     ```

### 2. **`>` (Greater than - Lớn hơn)**
   - **Mô tả**: So sánh hai giá trị, nếu giá trị bên trái lớn hơn giá trị bên phải thì trả về `true`, nếu không thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 > value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 10;
     if (x > 5) {
       // Điều kiện đúng vì x lớn hơn 5
     }
     ```

### 3. **`>=` (Greater than or equal to - Lớn hơn hoặc bằng)**
   - **Mô tả**: So sánh hai giá trị, nếu giá trị bên trái lớn hơn hoặc bằng giá trị bên phải thì trả về `true`, nếu không thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 >= value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 5;
     if (x >= 5) {
       // Điều kiện đúng vì x bằng 5
     }
     ```

### 4. **`<` (Less than - Nhỏ hơn)**
   - **Mô tả**: So sánh hai giá trị, nếu giá trị bên trái nhỏ hơn giá trị bên phải thì trả về `true`, nếu không thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 < value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 3;
     if (x < 5) {
       // Điều kiện đúng vì x nhỏ hơn 5
     }
     ```

### 5. **`<=` (Less than or equal to - Nhỏ hơn hoặc bằng)**
   - **Mô tả**: So sánh hai giá trị, nếu giá trị bên trái nhỏ hơn hoặc bằng giá trị bên phải thì trả về `true`, nếu không thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 <= value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 4;
     if (x <= 5) {
       // Điều kiện đúng vì x nhỏ hơn hoặc bằng 5
     }
     ```

### 6. **`!=` (Not equal to - Không bằng)**
   - **Mô tả**: So sánh hai giá trị, nếu chúng không bằng nhau thì trả về `true`, nếu chúng bằng nhau thì trả về `false`.
   - **Cú pháp**: 
     ```cpp
     value1 != value2
     ```
   - **Ví dụ**:
     ```cpp
     int x = 3;
     if (x != 5) {
       // Điều kiện đúng vì x không bằng 5
     }
     ```

### Tóm tắt các toán tử so sánh trong Arduino:

| Toán tử     | Mô tả                                | Ví dụ                                      |
|-------------|--------------------------------------|--------------------------------------------|
| `==`        | Bằng                                  | `if (x == 5)`                              |
| `>`         | Lớn hơn                               | `if (x > 5)`                               |
| `>=`        | Lớn hơn hoặc bằng                    | `if (x >= 5)`                              |
| `<`         | Nhỏ hơn                               | `if (x < 5)`                               |
| `<=`        | Nhỏ hơn hoặc bằng                    | `if (x <= 5)`                              |
| `!=`        | Không bằng                            | `if (x != 5)`                              |

### Ví dụ hoàn chỉnh:

```cpp
int a = 10;
int b = 20;

if (a == b) {
  // Không thực thi vì a không bằng b
}

if (a < b) {
  // Thực thi vì a nhỏ hơn b
}

if (a >= 10) {
  // Thực thi vì a lớn hơn hoặc bằng 10
}

if (a != b) {
  // Thực thi vì a không bằng b
}
```

Những toán tử so sánh này giúp bạn kiểm tra các điều kiện trong chương trình và điều khiển luồng thực thi dựa trên các phép so sánh giữa các giá trị.

# Bitwise Operators

Các **Bitwise Operators** (Toán tử Bitwise) trong Arduino (và C/C++) là các toán tử thao tác trực tiếp trên các bit của một số nguyên. Các toán tử này được sử dụng để thao tác với các bit trong một số nhị phân, có thể thay đổi hoặc kiểm tra các bit cụ thể trong một giá trị.

### Các toán tử Bitwise trong Arduino:

| Toán tử   | Mô tả                               | Ví dụ                                    |
|-----------|-------------------------------------|------------------------------------------|
| `<<`      | **Bitshift left** (Dịch trái)       | Dịch các bit sang bên trái (nhân với 2). |
| `>>`      | **Bitshift right** (Dịch phải)      | Dịch các bit sang bên phải (chia cho 2). |
| `&`       | **Bitwise AND** (Và bitwise)        | Kiểm tra các bit tương ứng là 1 trong cả hai số. |
| `~`       | **Bitwise NOT** (Không bitwise)     | Đảo ngược tất cả các bit.                |
| `|`       | **Bitwise OR** (Hoặc bitwise)       | Kiểm tra nếu ít nhất một trong các bit là 1. |
| `^`       | **Bitwise XOR** (Hoặc loại trừ bitwise) | Kiểm tra nếu các bit khác nhau (1 và 0 hoặc 0 và 1). |

### 1. **`<<` (Bitshift Left - Dịch trái)**:
   - **Mô tả**: Dịch các bit của một giá trị sang bên trái. Mỗi lần dịch sang trái, giá trị của số sẽ tăng gấp đôi (nhân với 2).
   - **Cú pháp**: `value << n` (Dịch bit của `value` sang trái n vị trí).
   - **Ví dụ**:
     ```cpp
     int x = 3; // 00000011 trong nhị phân
     int result = x << 2; // Dịch trái 2 bit, kết quả là 12 (001100)
     // result = 12
     ```

### 2. **`>>` (Bitshift Right - Dịch phải)**:
   - **Mô tả**: Dịch các bit của một giá trị sang bên phải. Mỗi lần dịch sang phải, giá trị của số sẽ giảm một nửa (chia cho 2).
   - **Cú pháp**: `value >> n` (Dịch bit của `value` sang phải n vị trí).
   - **Ví dụ**:
     ```cpp
     int x = 16; // 00010000 trong nhị phân
     int result = x >> 2; // Dịch phải 2 bit, kết quả là 4 (00000100)
     // result = 4
     ```

### 3. **`&` (Bitwise AND - Và bitwise)**:
   - **Mô tả**: Thực hiện phép toán "và" giữa các bit của hai số. Chỉ khi cả hai bit là 1, kết quả sẽ là 1, nếu không thì là 0.
   - **Cú pháp**: `value1 & value2`.
   - **Ví dụ**:
     ```cpp
     int a = 5;  // 0101 trong nhị phân
     int b = 3;  // 0011 trong nhị phân
     int result = a & b; // Kết quả là 1 (0001 trong nhị phân)
     // result = 1
     ```

### 4. **`~` (Bitwise NOT - Không bitwise)**:
   - **Mô tả**: Đảo ngược tất cả các bit của một giá trị, chuyển 1 thành 0 và 0 thành 1.
   - **Cú pháp**: `~value`.
   - **Ví dụ**:
     ```cpp
     int x = 5;  // 0101 trong nhị phân
     int result = ~x; // Kết quả là -6 (11111010 trong nhị phân đối với số nguyên có dấu)
     // result = -6
     ```

### 5. **`|` (Bitwise OR - Hoặc bitwise)**:
   - **Mô tả**: Thực hiện phép toán "hoặc" giữa các bit của hai số. Nếu ít nhất một trong hai bit là 1, kết quả sẽ là 1, nếu không thì là 0.
   - **Cú pháp**: `value1 | value2`.
   - **Ví dụ**:
     ```cpp
     int a = 5;  // 0101 trong nhị phân
     int b = 3;  // 0011 trong nhị phân
     int result = a | b; // Kết quả là 7 (0111 trong nhị phân)
     // result = 7
     ```

### 6. **`^` (Bitwise XOR - Hoặc loại trừ bitwise)**:
   - **Mô tả**: Thực hiện phép toán "hoặc loại trừ" giữa các bit của hai số. Kết quả sẽ là 1 nếu các bit khác nhau (1 và 0 hoặc 0 và 1), nếu các bit giống nhau, kết quả là 0.
   - **Cú pháp**: `value1 ^ value2`.
   - **Ví dụ**:
     ```cpp
     int a = 5;  // 0101 trong nhị phân
     int b = 3;  // 0011 trong nhị phân
     int result = a ^ b; // Kết quả là 6 (0110 trong nhị phân)
     // result = 6
     ```

### Tóm tắt các toán tử Bitwise trong Arduino:

| Toán tử   | Mô tả                                               | Ví dụ                                      |
|-----------|-----------------------------------------------------|--------------------------------------------|
| `<<`      | Bitshift left (Dịch trái)                           | `x << 2`                                   |
| `>>`      | Bitshift right (Dịch phải)                          | `x >> 2`                                   |
| `&`       | Bitwise AND (Và bitwise)                            | `a & b`                                    |
| `~`       | Bitwise NOT (Không bitwise)                         | `~x`                                       |
| `|`       | Bitwise OR (Hoặc bitwise)                           | `a | b`                                    |
| `^`       | Bitwise XOR (Hoặc loại trừ bitwise)                 | `a ^ b`                                    |

### Ví dụ hoàn chỉnh:
```cpp
int a = 5;  // 0101 trong nhị phân
int b = 3;  // 0011 trong nhị phân

int shiftLeft = a << 1;  // Dịch trái 1 bit, kết quả là 10 (1010 trong nhị phân)
int shiftRight = a >> 1; // Dịch phải 1 bit, kết quả là 2 (0010 trong nhị phân)

int bitwiseAnd = a & b;  // Kết quả là 1 (0001 trong nhị phân)
int bitwiseOr = a | b;   // Kết quả là 7 (0111 trong nhị phân)
int bitwiseXor = a ^ b;  // Kết quả là 6 (0110 trong nhị phân)
int bitwiseNot = ~a;     // Kết quả là -6 (11111010 trong nhị phân đối với số nguyên có dấu)
```

Các toán tử bitwise thường được sử dụng trong các tình huống cần tối ưu bộ nhớ hoặc xử lý trực tiếp các bit của dữ liệu, chẳng hạn như trong các giao thức truyền thông, mã hóa hoặc giải mã, hoặc các ứng dụng phần cứng cần thao tác với các bit.

# Further Syntax

### Các cú pháp cơ bản trong Arduino

Dưới đây là các cú pháp và ký hiệu phổ biến trong Arduino, cùng với giải thích và ví dụ cho từng cú pháp.

| Cú pháp       | Mô tả                                           | Ví dụ và giải thích                                                              |
|---------------|-------------------------------------------------|----------------------------------------------------------------------------------|
| `/* */`       | **Block comment** (Chú thích khối)               | Dùng để viết chú thích nhiều dòng. Mọi thứ trong dấu `/*` và `*/` sẽ bị bỏ qua khi biên dịch. |
| `{} `         | **Curly braces** (Dấu ngoặc nhọn)                | Dùng để nhóm các câu lệnh trong các cấu trúc điều khiển (if, for, function, etc.).  |
| `#define`     | **Preprocessor directive** (Chỉ thị tiền xử lý)  | Định nghĩa các hằng số hoặc macro để sử dụng trong chương trình.                 |
| `#include`    | **Preprocessor directive** (Chỉ thị tiền xử lý)  | Dùng để thêm các thư viện hoặc tệp tiêu đề vào chương trình.                     |
| `;`           | **Semicolon** (Dấu chấm phẩy)                    | Dùng để kết thúc một câu lệnh trong Arduino/C++.                                  |
| `//`          | **Single-line comment** (Chú thích một dòng)     | Chú thích cho một dòng, tất cả những gì sau `//` sẽ bị bỏ qua khi biên dịch.      |

### Giải thích chi tiết và ví dụ:

1. **`/* */` (Block comment - Chú thích khối):**
   - **Mô tả**: Được sử dụng để chú thích nhiều dòng trong chương trình.
   - **Ví dụ**:
     ```cpp
     /*
       Đây là một chú thích
       nhiều dòng trong Arduino.
     */
     int x = 10;  // Khai báo biến x
     ```

2. **`{}` (Curly braces - Dấu ngoặc nhọn):**
   - **Mô tả**: Dùng để nhóm các câu lệnh lại với nhau, thường thấy trong các cấu trúc điều khiển như `if`, `for`, hàm.
   - **Ví dụ**:
     ```cpp
     void setup() {
       // Câu lệnh trong hàm setup()
       pinMode(LED_BUILTIN, OUTPUT);
     }

     void loop() {
       // Câu lệnh trong hàm loop()
       digitalWrite(LED_BUILTIN, HIGH);
       delay(1000);
       digitalWrite(LED_BUILTIN, LOW);
       delay(1000);
     }
     ```

3. **`#define` (Preprocessor directive - Chỉ thị tiền xử lý):**
   - **Mô tả**: Dùng để định nghĩa các hằng số hoặc macro trong chương trình.
   - **Ví dụ**:
     ```cpp
     #define LED_PIN 13  // Định nghĩa chân LED là 13
     void setup() {
       pinMode(LED_PIN, OUTPUT);
     }
     ```

4. **`#include` (Preprocessor directive - Chỉ thị tiền xử lý):**
   - **Mô tả**: Dùng để thêm các thư viện bên ngoài hoặc tệp tiêu đề vào chương trình. Các thư viện này cung cấp các hàm và đối tượng hữu ích.
   - **Ví dụ**:
     ```cpp
     #include <Wire.h>  // Thêm thư viện Wire cho giao tiếp I2C
     ```

5. **`;` (Semicolon - Dấu chấm phẩy):**
   - **Mô tả**: Dùng để kết thúc một câu lệnh trong Arduino/C++. Mỗi câu lệnh phải kết thúc bằng dấu chấm phẩy.
   - **Ví dụ**:
     ```cpp
     int x = 5;  // Kết thúc câu lệnh bằng dấu chấm phẩy
     digitalWrite(LED_BUILTIN, HIGH);  // Câu lệnh này điều khiển LED bật
     ```

6. **`//` (Single-line comment - Chú thích một dòng):**
   - **Mô tả**: Dùng để chú thích cho một dòng duy nhất trong chương trình.
   - **Ví dụ**:
     ```cpp
     int x = 10;  // Biến x được gán giá trị 10
     ```

### Tóm tắt các cú pháp:

| Cú pháp       | Mô tả                                           | Ví dụ                                      |
|---------------|-------------------------------------------------|--------------------------------------------|
| `/* */`       | Chú thích khối, có thể viết nhiều dòng.           | `/* Đây là chú thích nhiều dòng */`        |
| `{}`          | Dấu ngoặc nhọn, dùng để nhóm các câu lệnh.       | `if (x > 10) { // Lệnh trong if }`         |
| `#define`     | Định nghĩa hằng số hoặc macro.                   | `#define LED_PIN 13`                       |
| `#include`    | Thêm thư viện hoặc tệp tiêu đề vào chương trình. | `#include <Wire.h>`                        |
| `;`           | Kết thúc câu lệnh.                               | `int x = 10;`                              |
| `//`          | Chú thích một dòng.                              | `// Đây là một chú thích`                  |

Những cú pháp trên là các thành phần cơ bản giúp lập trình Arduino dễ dàng hơn. Việc sử dụng chúng một cách đúng đắn sẽ giúp mã nguồn của bạn rõ ràng, dễ hiểu và dễ bảo trì.

# Boolean Operators

### Các toán tử Boolean trong Arduino

Toán tử Boolean là các toán tử dùng để xử lý giá trị đúng (true) hoặc sai (false). Các toán tử này thường được sử dụng trong các câu lệnh điều kiện để kiểm tra các điều kiện logic.

| Toán tử | Mô tả                               | Ví dụ và giải thích                                                            |
|---------|-------------------------------------|-------------------------------------------------------------------------------|
| `&&`    | **Logical AND** (Phép AND logic)   | Trả về `true` nếu cả hai điều kiện đều đúng.                                  |
| `!`     | **Logical NOT** (Phép phủ định logic) | Đảo ngược giá trị của điều kiện, nếu là `true` thì trở thành `false`, và ngược lại. |
| `||`    | **Logical OR** (Phép OR logic)     | Trả về `true` nếu ít nhất một trong các điều kiện đúng.                      |

### Giải thích chi tiết và ví dụ:

1. **`&&` (Logical AND - Phép AND logic):**
   - **Mô tả**: Toán tử này trả về `true` chỉ khi cả hai điều kiện đều đúng. Nếu có một điều kiện sai, kết quả sẽ là `false`.
   - **Ví dụ**:
     ```cpp
     int a = 5;
     int b = 10;

     if (a > 3 && b < 15) {
       // Cả hai điều kiện đều đúng, nên sẽ vào trong câu lệnh này
       digitalWrite(LED_BUILTIN, HIGH);
     }
     ```
   - Trong ví dụ trên, cả `a > 3` và `b < 15` đều đúng, vì vậy LED sẽ sáng.

2. **`!` (Logical NOT - Phép phủ định logic):**
   - **Mô tả**: Toán tử `!` đảo ngược giá trị của một điều kiện. Nếu điều kiện là `true`, toán tử `!` sẽ biến nó thành `false` và ngược lại.
   - **Ví dụ**:
     ```cpp
     bool isRaining = false;

     if (!isRaining) {
       // Điều kiện isRaining là false, nên phủ định nó thành true và vào trong câu lệnh
       digitalWrite(LED_BUILTIN, HIGH);
     }
     ```
   - Ở đây, `isRaining` là `false`, nhưng khi sử dụng toán tử `!`, giá trị của nó trở thành `true`, vì vậy LED sẽ sáng.

3. **`||` (Logical OR - Phép OR logic):**
   - **Mô tả**: Toán tử này trả về `true` nếu ít nhất một trong các điều kiện là đúng. Nếu tất cả các điều kiện đều sai, kết quả sẽ là `false`.
   - **Ví dụ**:
     ```cpp
     int a = 5;
     int b = 2;

     if (a > 3 || b > 3) {
       // Vì a > 3 đúng, nên toàn bộ điều kiện là true và vào trong câu lệnh
       digitalWrite(LED_BUILTIN, HIGH);
     }
     ```
   - Trong ví dụ này, điều kiện `a > 3` là đúng, vì vậy toán tử `||` trả về `true`, dù điều kiện `b > 3` là sai. LED sẽ sáng.

### Tóm tắt các toán tử Boolean:

| Toán tử | Mô tả                               | Ví dụ                                          |
|---------|-------------------------------------|-----------------------------------------------|
| `&&`    | Phép AND logic, trả về `true` khi cả hai điều kiện đều đúng. | `if (a > 3 && b < 15)`                        |
| `!`     | Phép phủ định logic, đảo ngược giá trị điều kiện.        | `if (!isRaining)`                             |
| `||`    | Phép OR logic, trả về `true` nếu ít nhất một điều kiện đúng. | `if (a > 3 || b > 3)`                         |

Các toán tử này giúp bạn xây dựng các câu lệnh điều kiện phức tạp trong chương trình Arduino, giúp kiểm tra các trạng thái và hành động dựa trên kết quả logic.

# Compound Operators

### Các toán tử hợp nhất (Compound Operators) trong Arduino

Các toán tử hợp nhất (compound operators) là các toán tử giúp thực hiện các phép toán và gán giá trị một cách ngắn gọn và hiệu quả hơn. Chúng giúp giảm bớt sự lặp lại trong mã nguồn và cải thiện tính dễ đọc của chương trình.

Dưới đây là bảng mô tả và ví dụ về các toán tử hợp nhất trong Arduino:

| Toán tử | Mô tả                                | Ví dụ và giải thích                                                        |
|---------|--------------------------------------|---------------------------------------------------------------------------|
| `+=`    | **Compound addition** (Cộng hợp nhất) | Tăng giá trị của biến lên một số và gán lại cho biến đó.                    |
| `&=`    | **Compound bitwise AND** (AND hợp nhất) | Thực hiện phép AND bitwise với giá trị hiện tại của biến và giá trị sau dấu `&`, rồi gán lại cho biến đó. |
| `|=`    | **Compound bitwise OR** (OR hợp nhất)  | Thực hiện phép OR bitwise với giá trị hiện tại của biến và giá trị sau dấu `|`, rồi gán lại cho biến đó. |
| `^=`    | **Compound bitwise XOR** (XOR hợp nhất) | Thực hiện phép XOR bitwise với giá trị hiện tại của biến và giá trị sau dấu `^`, rồi gán lại cho biến đó. |
| `/=`    | **Compound division** (Chia hợp nhất)   | Chia giá trị của biến cho một số và gán lại kết quả cho biến đó.            |
| `*=`    | **Compound multiplication** (Nhân hợp nhất) | Nhân giá trị của biến với một số và gán lại kết quả cho biến đó.           |
| `%=`    | **Compound remainder** (Phần dư hợp nhất) | Lấy phần dư khi chia giá trị của biến cho một số và gán lại kết quả cho biến đó. |
| `-=`    | **Compound subtraction** (Trừ hợp nhất) | Trừ một giá trị khỏi biến và gán lại kết quả cho biến đó.                  |
| `--`    | **Decrement** (Giảm giá trị)          | Giảm giá trị của biến đi một đơn vị.                                        |
| `++`    | **Increment** (Tăng giá trị)          | Tăng giá trị của biến lên một đơn vị.                                       |

### Giải thích chi tiết và ví dụ:

1. **`+=` (Compound addition)**:
   - **Mô tả**: Thực hiện phép cộng và gán lại kết quả vào biến ban đầu.
   - **Ví dụ**:
     ```cpp
     int a = 5;
     a += 3;  // Tương đương với a = a + 3;
     // a giờ sẽ có giá trị là 8.
     ```

2. **`&=` (Compound bitwise AND)**:
   - **Mô tả**: Thực hiện phép AND bitwise và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     byte a = 5;  // 0101 trong nhị phân
     a &= 3;      // 0011 trong nhị phân, kết quả là 0001, và a sẽ có giá trị 1.
     ```

3. **`|=` (Compound bitwise OR)**:
   - **Mô tả**: Thực hiện phép OR bitwise và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     byte a = 5;  // 0101 trong nhị phân
     a |= 3;      // 0011 trong nhị phân, kết quả là 0111, và a sẽ có giá trị 7.
     ```

4. **`^=` (Compound bitwise XOR)**:
   - **Mô tả**: Thực hiện phép XOR bitwise và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     byte a = 5;  // 0101 trong nhị phân
     a ^= 3;      // 0011 trong nhị phân, kết quả là 0110, và a sẽ có giá trị 6.
     ```

5. **`/=` (Compound division)**:
   - **Mô tả**: Thực hiện phép chia và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     int a = 10;
     a /= 2;  // Tương đương với a = a / 2;
     // a giờ sẽ có giá trị là 5.
     ```

6. **`*=` (Compound multiplication)**:
   - **Mô tả**: Thực hiện phép nhân và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     int a = 5;
     a *= 2;  // Tương đương với a = a * 2;
     // a giờ sẽ có giá trị là 10.
     ```

7. **`%=` (Compound remainder)**:
   - **Mô tả**: Thực hiện phép lấy phần dư và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     int a = 10;
     a %= 3;  // Tương đương với a = a % 3;
     // a giờ sẽ có giá trị là 1 (phần dư của 10 chia cho 3).
     ```

8. **`-=` (Compound subtraction)**:
   - **Mô tả**: Thực hiện phép trừ và gán lại kết quả vào biến.
   - **Ví dụ**:
     ```cpp
     int a = 10;
     a -= 4;  // Tương đương với a = a - 4;
     // a giờ sẽ có giá trị là 6.
     ```

9. **`--` (Decrement)**:
   - **Mô tả**: Giảm giá trị của biến đi một đơn vị.
   - **Ví dụ**:
     ```cpp
     int a = 5;
     a--;  // Tương đương với a = a - 1;
     // a giờ sẽ có giá trị là 4.
     ```

10. **`++` (Increment)**:
    - **Mô tả**: Tăng giá trị của biến lên một đơn vị.
    - **Ví dụ**:
      ```cpp
      int a = 5;
      a++;  // Tương đương với a = a + 1;
      // a giờ sẽ có giá trị là 6.
      ```

### Tóm tắt các toán tử hợp nhất:

| Toán tử | Mô tả                                 | Ví dụ                                          |
|---------|---------------------------------------|-----------------------------------------------|
| `+=`    | Cộng hợp nhất                         | `a += 3;`                                      |
| `&=`    | AND hợp nhất bitwise                  | `a &= 3;`                                      |
| `|=`    | OR hợp nhất bitwise                   | `a |= 3;`                                      |
| `^=`    | XOR hợp nhất bitwise                  | `a ^= 3;`                                      |
| `/=`    | Chia hợp nhất                         | `a /= 2;`                                      |
| `*=`    | Nhân hợp nhất                         | `a *= 2;`                                      |
| `%=`    | Phần dư hợp nhất                      | `a %= 3;`                                      |
| `-=`    | Trừ hợp nhất                          | `a -= 4;`                                      |
| `--`    | Giảm giá trị một đơn vị               | `a--;`                                         |
| `++`    | Tăng giá trị một đơn vị               | `a++;`                                         |

Các toán tử hợp nhất này giúp bạn viết mã gọn gàng và dễ đọc hơn khi thực hiện các phép toán cơ bản với các biến trong chương trình Arduino.