# HW1

<div align="right"><font size="4">2019732021 강용이</font></div>


---

### P2.7

<a href="https://ibb.co/9tk3xpj"><img src="https://i.ibb.co/sHdJTgr/image.png" alt="image" border="0"></a>


$$v_2(t) = -v_1(t)\int_{0}^{t}\frac{dt}{RC}$$  
위 수식에 라플라스 변환을 적용하면  
$$V_2(s) = -\frac{V_1(s)}{sRC}$$  
이 되고 전달함수는  
$$G(s) = \frac{V_2(s)}{V_1(s)} = \frac{1}{sRC}$$
이다.

---

### P2.12


<a href="https://ibb.co/fDC69HK"><img src="https://i.ibb.co/KK94DWQ/2024-10-07-201600.jpg" alt="2024-10-07-201600" border="0"></a>

$$\frac{Y(s)}{R(s)} = \frac{K}{s+50}$$  
여기서 단위계단 입력이므로
$$R(s) = \frac{1}{s}$$

이다.

$$Y(s) = \frac{k}{s(s+50)} = \frac{k}{50}(\frac{1}{s}-\frac{1}{s+50})$$

이고, 역라플라스 변환을 진행하면

$$y(t) = \frac{k}{50}(1-e^{-50t})$$

이고,  
$$\displaystyle \lim_{t\to\infty}y(t) =\frac{k}{50}=1$$  
이다. 따라서 $$k = 50$$

---

### P2.15

<a href="https://imgbb.com/"><img src="https://i.ibb.co/DWgbts8/2024-10-07-211144.jpg" alt="2024-10-07-211144" border="0"></a>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/jr3vPkx/2024-10-07-211241.jpg" alt="2024-10-07-211241" border="0"></a>


추의 중력, 에너지 손실기, 스프링 장력

$$m\frac{d^2x(t)}{dt^2}+b\frac{dx(t)}{dt}+kx(t)=0$$  
라플라스 변환  
$$ms^2X(s)+bsX(s)+kX(s) = 0$$

$$X(s) = \frac{1}{ms^2 + bs + k}$$

역라플라스 변환  
매트랩 코드

```
clear;
% 변수 생성
syms s t m b k X_s X_t

% 식 정의
X_s = 1/(m*s^2+b*s+k)

% 역라플라스 변환
x_t = ilaplace(X_s, s, t)
```


$$
x(t)=\frac{2 \sin \left( \frac{t \sqrt{- b^2 + 4 k m}}{2 m} \right) e^ \left( -\frac{b t}{2 m} \right)}{\sqrt{- b^2 + 4 k m}}
$$

---

### P2.26


<img src="https://i.ibb.co/n12LcgB/2024-10-07-215549.jpg" alt="2024-10-07-215549" border="0">

스프링-질량-감쇄기 모델 식

$$F(t) = M\frac{\mathrm{d^2x(t)}}{\mathrm{d} x^2} +b(\frac{\mathrm{dx(t)} }{\mathrm{d} x} -\frac{\mathrm{dy(t)} }{\mathrm{d} x}) + k(x(t)-y(t))$$

$$0 = m\frac{\mathrm{d^2y(t)}}{\mathrm{d} x^2} +b( \frac{\mathrm{dy(t)} }{\mathrm{d} x} -\frac{\mathrm{dx(t)} }{\mathrm{d} x}) + k(y(t)-x(t))$$

라플라스 변환 적용

$$F(s) = Ms^2X(s) +bsX(s) + kX(s) - bsY(s) - kY(s)$$

$$0 = ms^2Y(s) +bsY(s) + kY(s) - bsX(s) - kX(s)$$

와 같이 된다. 이를 행렬 식으로 작성하면

$$\begin{pmatrix}
Ms^s+bs+k & -bs-k \\
 -bs-k  & ms^2+bs+k
\end{pmatrix}\begin{pmatrix}
X(s) \\
 Y(s)
\end{pmatrix}=\begin{pmatrix}
F(s) \\
 0
\end{pmatrix}$$


매트랩 코드

```
% 변수 생성
syms M m s b k X_s Y_s F_s

% 행렬 입력
A = [M*s^2+b*s+k -b*s-k;-b*s-k m*s^2+b*s+k]
B = [X_s;Y_s]
C = [F_s;0]

% B행렬 계산
sol = inv(A) * C

% B행렬의 2번째(Y_s)/F_s 도출
YOF = sol(2) / F_s
pretty(YOF)
```


위 연산의 결과로 전달함수 $\frac{Y(s)}{F(s)}$는


$$G(S) = \frac{Y(s)}{F(s)} = \frac{k+bs}{bms^3+kms^2+bMs^3+kMs^2+Mms^4}$$

---

### P2.37

<a href="https://imgbb.com/"><img src="https://i.ibb.co/dk5sP9M/2024-10-08-153849.jpg" alt="2024-10-08-153849" border="0"></a>  
<a href="https://imgbb.com/"><img src="https://i.ibb.co/7GFtR9x/2024-10-08-153904.jpg" alt="2024-10-08-153904" border="0"></a>

미분방정식 작성

$$m_{1}\frac{\mathrm{d^2}x(t)}{\mathrm{d} t} + k_1x(t) + k_2(x(t)-y(t)) = 0$$

$$m_{2}\frac{\mathrm{d^2}y(t)}{\mathrm{d} t} + k_2(y(t)-x(t)) = u(t)$$

$m_1 = m_2 = K_1 = K_2 = 1$ 대입

$$\frac{\mathrm{d^2}x(t)}{\mathrm{d} x} = -2x(t) + y(t)$$

$$\frac{\mathrm{d^2}y(t)}{\mathrm{d} t} = u(t) + x(t) -y(t)$$


## (b)

라플라스 변환 적용

$$s^2X(s) = -2X(s) + Y(s)$$

$$\to (s^2+2)X(s) - Y(s) = 0$$

$$s^2Y(s) = U(s) + X(s) - Y(s)$$

$$\to -X(s) + (s^2 + 1)Y(s) = U(s)$$

행렬형태로 작성

$$
\begin{pmatrix}s^2+2 &-1  \\
-1 & s^2+1 \\
\end{pmatrix}  \begin{pmatrix}
X(s) \\
 Y(s)
\end{pmatrix} = \begin{pmatrix}
0 \\
 U(s)
\end{pmatrix}
$$

Y(s), 전달함를 구하는 매트랩 코드

```
% 변수 생성
clear;
syms X_s Y_s U_s s

% 행렬 선언
A = [s^2+2 -1;-1 s^2+1]
B = [X_s;Y_s]
C = [0;U_s]

% Y_s 계산
sol = inv(A)*C

% 전달함수 계산
resol = C(2)/sol(2)

```

$$\frac{Y(s)}{U(s)} = \frac{s^2+2}{s^4+3s^2+1}$$
