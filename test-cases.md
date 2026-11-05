# Test cases for the billing app

Say each line in order, tapping the mic each time (or type it). The last line says "bill". Compare the receipt with the expected one.

## Case 1 - Grams, kilo and a repeated item

Say, in order:

1. "tomato 300 gms"
2. "onion two kilo"
3. "tomato 300 gms"
4. "bill"

Tomato 300 g said twice merges into one line (0.600 kg). Onion 2 kg.

Expected receipt:

```
             ABIRAMI STORE
      6/47 perummal kovil street,
         Rajankuppam,Chennai-95
               9940016226
        GST No : 33BFGPN4893C1ZF
----------------------------------------
BillNo : 1    Date : 05/11/2026 02:30:PM
Cashier : CASHIER1  BillType : CASH BILL
----------------------------------------
SNO DESCRIPTION
              QTY      RATE       AMOUNT
----------------------------------------
1   TOMATO
            0.600     30.00        18.00
2   ONION
            2.000     40.00        80.00
----------------------------------------
             Gross Amount :        98.00
                  Coinage :         0.00
             Total Amount :        98.00
----------------------------------------
Total Items : 2          Total Qty : 2.6
----------------------------------------
           DOOR DELIVERY FREE
               8608687575
           WHATSAPP/ GPAY NO
         9940016226/8667695433
     Thank You !!!.Visit Again !!!.
```

## Case 2 - Pieces, packets and Atta

Say, in order:

1. "banana five"
2. "milk two"
3. "aavin one"
4. "atta two"
5. "bill"

Counted items: banana, milk packets, Aavin packet, Atta packets.

Expected receipt:

```
             ABIRAMI STORE
      6/47 perummal kovil street,
         Rajankuppam,Chennai-95
               9940016226
        GST No : 33BFGPN4893C1ZF
----------------------------------------
BillNo : 1    Date : 05/11/2026 02:30:PM
Cashier : CASHIER1  BillType : CASH BILL
----------------------------------------
SNO DESCRIPTION
              QTY      RATE       AMOUNT
----------------------------------------
1   BANANA
                5      6.00        30.00
2   MILK
                2     28.00        56.00
3   AAVIN RED
                1     32.00        32.00
4   ATTA 1KG
                2     73.00       146.00
----------------------------------------
             Gross Amount :       264.00
                  Coinage :         0.00
             Total Amount :       264.00
----------------------------------------
Total Items : 4           Total Qty : 10
----------------------------------------
           DOOR DELIVERY FREE
               8608687575
           WHATSAPP/ GPAY NO
         9940016226/8667695433
     Thank You !!!.Visit Again !!!.
```

## Case 3 - Inactive item rejected, pomegranate

Say, in order:

1. "rice two kilo"
2. "pomegranate 500"
3. "pomegranate one kilo"
4. "bill"

Rice is inactive, so it is rejected with a message and not added. Pomegranate 500 g and 1 kg show as two lines.

Expected receipt:

```
             ABIRAMI STORE
      6/47 perummal kovil street,
         Rajankuppam,Chennai-95
               9940016226
        GST No : 33BFGPN4893C1ZF
----------------------------------------
BillNo : 1    Date : 05/11/2026 02:30:PM
Cashier : CASHIER1  BillType : CASH BILL
----------------------------------------
SNO DESCRIPTION
              QTY      RATE       AMOUNT
----------------------------------------
1   MADHULAI BIG
            0.500    350.00       175.00
2   MADHULAI BIG
            1.000    350.00       350.00
----------------------------------------
             Gross Amount :       525.00
                  Coinage :         0.00
             Total Amount :       525.00
----------------------------------------
Total Items : 2          Total Qty : 1.5
----------------------------------------
           DOOR DELIVERY FREE
               8608687575
           WHATSAPP/ GPAY NO
         9940016226/8667695433
     Thank You !!!.Visit Again !!!.
```

## Case 4 - Tamil words and grams

Say, in order:

1. "தக்காளி இரண்டு கிலோ"
2. "புடலங்காய் அரை கிலோ"
3. "பீர்க்கங்காய் 300 கிராம்"
4. "பில் போடு"

Speak in Tamil. This one rounds down: Coinage -0.40, total 118.

Expected receipt:

```
             ABIRAMI STORE
      6/47 perummal kovil street,
         Rajankuppam,Chennai-95
               9940016226
        GST No : 33BFGPN4893C1ZF
----------------------------------------
BillNo : 1    Date : 05/11/2026 02:30:PM
Cashier : CASHIER1  BillType : CASH BILL
----------------------------------------
SNO DESCRIPTION
              QTY      RATE       AMOUNT
----------------------------------------
1   TOMATO
            2.000     30.00        60.00
2   PODALANKAI
            0.500     64.00        32.00
3   PIRKKANGAI
            0.300     88.00        26.40
----------------------------------------
             Gross Amount :       118.40
                  Coinage :        -0.40
             Total Amount :       118.00
----------------------------------------
Total Items : 3          Total Qty : 2.8
----------------------------------------
           DOOR DELIVERY FREE
               8608687575
           WHATSAPP/ GPAY NO
         9940016226/8667695433
     Thank You !!!.Visit Again !!!.
```

## Case 5 - Two items in one sentence, default 1 kg, customer number

Say, in order:

1. "tomato two kilo onion three kilo"
2. "carrot"
3. "number nine nine four zero zero one six two two six"
4. "bill"

Two items in one sentence, carrot with no quantity (1 kg), and a customer number (shows the Customer line).

Expected receipt:

```
             ABIRAMI STORE
      6/47 perummal kovil street,
         Rajankuppam,Chennai-95
               9940016226
        GST No : 33BFGPN4893C1ZF
----------------------------------------
BillNo : 1    Date : 05/11/2026 02:30:PM
Cashier : CASHIER1  BillType : CASH BILL
Customer : 99400 16226
----------------------------------------
SNO DESCRIPTION
              QTY      RATE       AMOUNT
----------------------------------------
1   TOMATO
            2.000     30.00        60.00
2   ONION
            3.000     40.00       120.00
3   CARROT
            1.000     60.00        60.00
----------------------------------------
             Gross Amount :       240.00
                  Coinage :         0.00
             Total Amount :       240.00
----------------------------------------
Total Items : 3            Total Qty : 6
----------------------------------------
           DOOR DELIVERY FREE
               8608687575
           WHATSAPP/ GPAY NO
         9940016226/8667695433
     Thank You !!!.Visit Again !!!.
```

## Rejected item check

Say "rice two kilo" (Rice is inactive). The red message should read: "புரியவில்லை: "rice two kilo" — மீண்டும் சொல்லுங்கள் அல்லது தட்டச்சு செய்யவும்" and nothing is added to the cart.
