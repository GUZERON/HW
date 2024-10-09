<a href="https://ibb.co/XYxGycG"><img src="https://i.ibb.co/GHQrszr/image.png" alt="image" border="0"></a>

(a) 상태 변수로 표현된 1차 미분 방정식을 구하기 위해서, 적당한 상태변수는 $x_1(t)=$변위 와 $x_2(t)=$속도로 설정한다.

(b) 상태 변수로 1차 미분 방정식을 구현하면,

$$x_1(t)=y(t) $$

$$x_2(t)=\frac{y(t)}{dt}$$

이 되고, 질량, 마찰력, 스프링의 탄성에 대한 운동 방정식을 작성하게 되면

$$M\frac{\mathrm{d^2}y(t) }{\mathrm{d} t^2}+b\frac{\mathrm{d}y(t) }{\mathrm{d} t}+ky(x)=r(t)$$

이 된다.

(c) 상태 미분 방정식은 변위를 미분하면 속도가 되기 때문에, 이를 식으로 나타내면


$$x_2(t)=\frac{y(t)}{dt}=\frac{dx_1(t)}{dt}$$ 이고,

$$\frac{dx_2(t)}{dt}=-\frac{b}{m}x_2(t)+\frac{k}{m}x_1(t)+\frac{1}{M}r(t)$$ 이 된다.


<a href="https://imgbb.com/"><img src="https://i.ibb.co/RYpxjj4/image.png" alt="image" border="0"></a>

우선 상태변수는

$$x_1(t)=i_L(t), x_2(t)=V_c(t) $$

이고,

KCL과 KVL을 이용해서 RLC회로를 해석하게 되면,


$$C\frac{dV_c}{dt}=i_R-i_L$$

$$R*i_R=V_2-V_c$$

가 된다. 이를 식을 정리하면,

$$\frac{dx_2(t)}{dt}=\frac{V_2}{RC}-\frac{x_2(t)}{RC}-\frac{x_1(t)}{R}$$

$$\frac{dx_1(t)}{dt}=\frac{V_1}{L}-\frac{V_2}{L}+\frac{x_2(t)}{L}$$

이고, 이를 행렬로 정리하면,
$$
\begin{pmatrix} \dot{x_1} \\ \dot{x_2} \end{pmatrix} = \begin{bmatrix} 0 & 1/c \\ -1/c & -1/RC \end{bmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} + \begin{bmatrix} 1/L & -1/L \\ 0 & 1/RC \end{bmatrix} \begin{pmatrix} V_1 \\ V_2 \end{pmatrix}
$$
이다.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/DgdnL8L/image.png" alt="image" border="0"></a>

(a) 폐루프의 전달 함수는 구하게 되면, 한번 반환 되는 부분을 잘 생각해야한다. 이를 통해 식을 세우면,

$$T(s)=\frac{Y(s)}{R(s)}=\frac{G(s)}{1+G(s)}=\frac{\frac{s+2}{s^3+5s^2-24s}}{1+\frac{s+2}{s^3+5s^2-24s}}=\frac{s+2}{s^3+5s^2-23s+2}$$

가 된다.

(b) 이를 통해 상태모델과 phase variable form으로 작성하면,

$$A=
\begin{bmatrix}
0&1&0 \\\\
0&0&1 \\\\
-2&23&-5
\end{bmatrix}$$

$$B=
\begin{bmatrix}
0\\\
0\\\
1
\end{bmatrix}$$

$$C=
\begin{bmatrix}
2&1&0
\end{bmatrix}$$

이므로,
$$
\dot{x}(t) = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -2 & 23 & -5 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} u(t)
$$

$$
y(t) = \begin{bmatrix} 2 & 1 & 0 \end{bmatrix} x(t)
$$

<a href="https://imgbb.com/"><img src="https://i.ibb.co/b344f76/image.png" alt="image" border="0"></a>

(a) 상태 공간 모델을 구하게 되면,
$$
Y(s) = (8s + 40) z(s)
$$

$$
R(s) = (s^3 + 12s^2 + 44s + 48) z(s)
$$

$$
\dot{x}(t) = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -48 & -44 & -12 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} r(t)
$$

$$
y(t) = \begin{bmatrix} 40 & 8 & 0 \end{bmatrix} x(t)
$$

(b) 상태 천이 행렬을 구하는 식은

$$A=
\begin{bmatrix}
0&1&0 \\\\
0&0&1 \\\\
-48&-44&-12
\end{bmatrix}$$
$$ B=
\begin{bmatrix}
0\\\\
0\\\\
1
\end{bmatrix}$$
$$c=
\begin{bmatrix}
40&8&0
\end{bmatrix}$$

$
\dot{x} = A x(t) + B r(t), \
$
$
y(t) = CX(t)
$

$
SX(s)-x(0)=AX(s)+BR(s)→X(s)=\frac{B}{SI-A}R(s)+\frac{1}{SI-A}x(0)
$

$
→X(t) = \mathrm{e^{At}}x(0)+S\mathrm{e^{A(t-τ)}}Bu(t)dt
$

$
\Phi(t)=\mathrm{e^{At}}
$
이 된다.  
이를 매트랩을 이용하여 상태 천이 행렬을 구하는 방식은 아래와 같다.

syms s t   
SI =[s -1 0; 0 s -1; 48 44 s+12]   
PS=SI^-1  
PT = ilaplace(PS);  
PT

<a href="https://ibb.co/HD2Q1Cr"><img src="https://i.ibb.co/QFcGzk6/image.png" alt="image" border="0"></a>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/nQSD1vK/image.png" alt="image" border="0"></a>   

$ \dot{X}(t) = A X(t) + B u(t), \quad Y(t) = C x(t) + D u(t) $

라플라스 변환을 적용하면:

$ sX(s) = A X(s) + B U(s) $

$ Y(s) = C X(s) + D U(s) $

정리하면:

$ X(s) = \frac{B U(s)}{sI - A} $

$ Y(s) = \frac{C B U(s)}{sI - A} + D U(s) = \left(\frac{C B}{sI - A} + D \right) U(s) $

$ G(s) = \frac{Y(s)}{U(s)} = \frac{C B}{sI - A} + D $

예시:

$ A = \begin{pmatrix} 1 & 1 & -1 \\ 4 & 3 & 0 \\ -2 & 1 & 0 \end{pmatrix}, \quad
B = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}, \quad
C = \begin{pmatrix} 1 & 0 & 0 \end{pmatrix}, \quad
D = 0 $

$ sI = \begin{pmatrix} s & 0 & 0 \\ 0 & s & 0 \\ 0 & 0 & s \end{pmatrix} $
