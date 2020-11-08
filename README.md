# Matlab_diffex
# roundoff, truncation error 확인하기
## 1. roundoff error, truncation error
roundoff error: 수가 컴퓨터에 저장될 때 비트단위로 저장이 되어 실제 수와 다르게 저장되는 경우
truncation error: 테일러 급수등으로 근사치를 구할때 항을 어디까지 구하는가에 따라 나타나는 오차

## 2.코드 작성

함수선언

    function diffex(func,dfunc,x,n)

초기값 설정      
H: step size        
D: finite difference        
E: true error

        format long
        dftrue=dfunc(x);
        h=1;
        H(1)=h;
        D(1)=(func(x+h)-func(x-h))/(2*h);
        E(1)=abs(dftrue-D(1));

step size를 1/10배로 줄여가면서 error값을 계산한다.

        for i=2:n
        h=h/10;
        H(i)=h;
        D(i)=(func(x+h)-func(x-h))/(2*h);
        E(i)=abs(dftrue-D(i));
        end
        
결과값 출력

        L=[H' D' E']';
        fprintf('    step size   finite difference    true error\n');
        fprintf('%14.10f %16.14f %16.13f\n',L);
        loglog(H,E),xlabel('Step Size'),ylabel('Error')
        title('Plot of Error Versus Step Size')
        format short
