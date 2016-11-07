nc chatbot.svattt.org 5555
Ask chatbot for the flag.

xin chào các bạn hôm nay mình xin viết write up về bài OTP-chatbot trong đợt thi svattt vừa qua
mình xin bỏ qua phần suy nghĩ và tập trung vào giải quyết yêu cầu
yêu cầu đầu tiên đó là tìm Encrypt_key
  while True:
    msg = raw_input("> ")
    if 'FLAG?' in msg:
        res = FLAG
    elif 'hello' in msg or 'hi' in msg or 'good' in msg or 'chao' in msg:
        res = greet[random.randrange(0,len(greet))]
    else:
        res = 'What?!? ' + randbyte(10)
    enc = encrypt(b2n(res), encrypt_key)
    print enc
    
  enc = b2n(res)**0x10001 mod encrypt_key
  => b2n(res)**0x10001 - enc = K*encrypt_key

nếu nhập hello, hi, goog, chao thì mình sẽ biết được b2n(res) = b2n(greet) 
với greet = ["'sup bro", "hey", "*nods*", "hey you get my snap?"] 
  b2n(greet[0])**0x10001 - enc1 = K1.encrypt_key 
  b2n(greet[1])**0x10001 - enc2 = K2.encrypt_key
  b2n(greet[2])**0x10001 - enc3 = K3.encrypt_key
  b2n(greet[3])**0x10001 - enc4 = K4.encrypt_key

==> encrypt_key = gcd(b2n(greet[0])**0x10001 - enc1,gcd(b2n(greet[1])**0x10001,gcd(b2n(greet[2])**0x10001,b2n(greet[3])**0x10001)))

Tìm được encrypt_key mình đi factor => và sử dụng công thức 
bây giờ bài toán trở về 1 bài RSA thông thường với N = encrypt_key
flag = enc_flag**d mod N => flag 

lưu ý: không phải encrypt_key nào cũng factor được bạn nên thử nhiều hơn 1 lần để có thể tìm được 1 cái encrypt_key có thể factor được
  
  

