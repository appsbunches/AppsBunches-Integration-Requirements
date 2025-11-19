# Recommendations for Integrating Services into Apps Bunches Mobile Application

## 1. Business Cycle Requirements

To ensure smooth integration of your app service into the Apps Bunches
mobile application, please provide the following:

### **App Information**

-   Full description of the app and its features
-   App URL in Zid Apps Market
-   Support email and official website (if available)

### **Media & Demonstration**

-   Introductory video explaining the app's service
-   Clear indication of where the service should appear in the mobile
    app
    (e.g., product page, checkout, order success page)

### **User Stories**

Provide: 
- A user story describing how the service works on the **Zid web store** 
- A user story describing how the service should work on the **Apps Bunches mobile app**

#### **Examples**

##### Chatbot SDK

    Open the app → Open the home page → Click on SDK chat icon

##### Upselling SDK

    Open the app → Open the cart page → Upselling bottom sheet appears automatically → User adds product to cart

##### Loyalty Program SDK

    Open the app → Open the home page → Points widget should appear
    Open the app → Open the account page → Points widget should appear

------------------------------------------------------------------------

## 2. Technical Requirements

### **Flutter SDK Development**

-   Developers must build a **Flutter SDK** to integrate their service
    with Apps Bunches mobile app
-   SDK must include **full usage documentation**
-   SDK must be published on **pub.dev**

### **Configuration & Initialization**

-   SDK must accept initial configuration values in **JSON**
-   SDK must support **sandbox mode** for testing
-   Sensitive data must be **encrypted**
-   SDK must support the latest **Flutter stable version**

### **Integration with Zid APIs**

SDK must receive configuration JSON from:

    GET /api/v1/scripts
    GET https://api.zid.sa/v2/catalog/stores/$storeId/layout-setting

JSON includes: - App status
- Tokens, IDs
- Colors
- Any required values

### **Initialization Method Example**

``` dart
APPSDKNAME.init(initialJson: {
  'status': true,
  'token': '123456890',
})
.onSuccess((value) => print(value))
.onCatchError((e) => print(e));
```

------------------------------------------------------------------------

## 3. Optional Features

### **Page Listener**

``` dart
APPSDKNAME.trackPageRoute(pageName: "wishlist");
```

### **Cart Events (CRUD)**

``` dart
APPSDKNAME.sendEvent(
  cartEvent: CartEvents(
    onAddToCart: (itemCartId) {},
    onDeleteToCart: (itemCartId) {},
  ),
);
```

### **UI Integration**

SDK may provide dialogs, bottom sheets, or custom widgets.

#### Example:

``` dart
Column(
 children: [
   OrderSuccessHeaderWidget(orderId: widget.orderId),
   OrderDetailsButtonWidget(orderId: widget.orderId),
   APPSDKNAME.orderDetailsWidget(),
   SizedBox(height: 30),
   TransferPaymentWidget(orderId: widget.orderId),
   SizedBox(height: 30),
   VatInfoWidget(),
 ],
);
```

------------------------------------------------------------------------

### **Search Events**

``` dart
List<Products> products = await APPSDKNAME.getProducts(q: 'Search Item');
```

------------------------------------------------------------------------

### **Abandoned Cart Events**

``` dart
APPSDKNAME.addCartUpdates(
  deviceId: '123456789',
  customerObject: {},
  cartObject: {},
  phase: 'add_to_cart',
);
```

------------------------------------------------------------------------

### **Customer Support Widgets (ChatBot, WhatsApp, etc.)**

``` dart
floatingActionButton: APPSDKNAME.showFloatingActionButton();
```

------------------------------------------------------------------------

### **Cashback / Exchange / Return Events**

``` dart
APPSDKNAME.showWidgets();

APPSDKNAME.return(
  mobileNumber: '+966666',
  userID: '',
  orderModel: {},
);
```

------------------------------------------------------------------------

## 4. Targeted App Categories

This document applies to: 
- Customer Support Apps
- Marketing Apps
- Operations
- Other service apps

------------------------------------------------------------------------

## 5. Note

All examples are illustrative and may be modified based on service
requirements.
