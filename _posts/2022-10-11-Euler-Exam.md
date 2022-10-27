Examen 

---
layout: post
title: Método de Euler Mejorado 
---

## Método de Euler ##

Este método ajusta el error de método estándar de Euler, el cuál se basa en generar un valor **predictor**, que corresponde al primer cálculo, en **i**, a continuación se genera un valor **corrector** que en realidad es el cálculo de la pendiente en el punto **i+1**

Ocuparemos la siguiente expresión para **Euler-Predictor** :

**𝒚𝒑𝒊+𝟏 = 𝒚𝒊 + 𝒇 𝒙𝒊 , 𝒚𝒊 𝒉**

Y la siguiente para **Euler-Corrector** :
**yi+1 =y𝒊 + h/2 (f(xi,yi) + f(xi+1, ypi+1))** (tomamos el predictor en y, que es un valor aproximado)

#### Gráfico de Método de Euler Mejorado 

![_config.yml]({{ site.baseurl }}/images/metodo_euler_mejorado.JPG
![_config.yml]({{ site.baseurl }}/images/metodo_euler_mejorado.JPG)

El método numérico de Euler Mejorado se aplicará a la siguiente forma de ecuación diferencial: **y’ = f(x,y)**

![_config.yml]({{ site.baseurl }}/images/ejercicio1.JPG
![_config.yml]({{ site.baseurl }}/images/ejercicio1.JPG)

A continuación se muestra el desarrollo del programa: 

```c++
#include <iostream>
#include <cmath>
using namespace std;

#define F(x,y) ((pow(x,3)*exp(-2*(x)))-(2*(y)))
#define G(x,y) ((exp(-2*(x))/4)*(pow(x,4)+4))

/*Como en el ejemplo de Euler mejorado, ambas funciones
 utilizan la Y resultante de la formula correctiva para el siguiente ciclo*/

//Euler predictivo
float eulerpred(float x, float y, float h)
{
  float result;
  result = y+(F(x,y)*h);
  return result;
}

//Euler mejorado
float eulermej(float x, float y, float h, float xi, float yi)
{
  float result;
  result = y+((h/2)*(F(x,y)+F(xi,yi)));
  return result;
}

int main()
{
  //X0, Y0 e intervalo H
  float x=0.0, y=1, h=0.1;
  float result, real;

  //Headers
  cout << "X," << "True Y," << "Predictive Euler Y," << "%P.Error,";
  cout << "Corrective Euler Y," << "%C.Error" << endl;

  //Primera fila
  cout << x << "," << G(x,y) << "," << y << "," << "0," << y << ",0"<< endl;
  
  //Loop de euler
  for (x=0.1;x<1.01;x+=h)
    {
      real = G(x,y);
      result = eulerpred(x,y,h);
      cout << x << "," << real << "," << result << "," << ((real-result)/real)*100;
      result = eulermej(x,y,h,(x+h),result);
      cout << "," << result << "," << ((real-result)/real)*100 << endl;
      y=result;
    }

  return 0;
}
```

****

Author: _EGM_
