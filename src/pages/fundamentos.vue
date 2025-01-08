<template>
  <v-container>
    <v-card>
      <template v-slot:title>
        <span class="font-weight-black">Método McCabe-Thiele</span>
      </template>
      <v-card-text class="bg-surface-light pt-4">
        <h2>Fundamento.</h2>
        <p>Tanto el método de McCabe-Thiele como el presente programa se
          fundamentan primordialmente en un diagrama de equilibrio, basado a su
          vez en la volatilidad relativa (α). Para una mezcla binaria, la curva de
          equilibrio toma la siguiente forma:</p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th>
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <mi>y</mi>
                    <mo>=</mo>
                    <mfrac>
                      <mrow>
                        <mi>α</mi>
                        <mi>x</mi>
                      </mrow>
                      <mrow>
                        <mn>1</mn>
                        <mo>+</mo>
                        <mrow>
                          <mo stretchy="true" form="prefix">(</mo>
                          <mi>α</mi>
                          <mo>−</mo>
                          <mn>1</mn>
                          <mo stretchy="true" form="postfix">)</mo>
                        </mrow>
                        <mi>x</mi>
                      </mrow>
                    </mfrac>
                  </mrow>
                  <annotation encoding="application/x-tex">y = \frac{\alpha x}{1 + (\alpha - 1)x}</annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 1)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <p>Donde:</p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>x</mi>
              <annotation encoding="application/x-tex">x</annotation>
            </semantics>
          </math>
          = fracción molar del componente más volátil en la fase líquida.
        </p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>y</mi>
              <annotation encoding="application/x-tex">y</annotation>
            </semantics>
          </math>
          = fracción molar del componente más volátil en la fase de vapor.
        </p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>α</mi>
              <annotation encoding="application/x-tex">\alpha</annotation>
            </semantics>
          </math>
          = volatilidad relativa. Mide qué tan más volátil es uno de los
          componentes con respecto a otro.
        </p>
        <p>En el diagrama de equilibrio, también se dibuja una línea diagonal,
          con pendiente igual a uno, representada por la ecuación:</p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th
              style="text-align: center;">
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <mi>y</mi>
                    <mo>=</mo>
                    <mi>x</mi>
                  </mrow>
                  <annotation encoding="application/x-tex">y = x</annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 2)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <p>Trazar o plotear la ecuación 1 y la ecuación 2 constituye la primera
          tarea a efectuar.</p>
        <p>Adicionalmente, se deben representar los puntos correspondientes a la
          concentración del componente más volátil en la corriente de fondo
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>B</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{B}</annotation>
            </semantics>
          </math>
          ),
          la concentración del componente más volátil en la alimentación
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>F</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{F}</annotation>
            </semantics>
          </math>
          ),
          y la concentración del componente más volátil en el destilado
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{D}</annotation>
            </semantics>
          </math>
          ).
        </p>
        <p>El punto correspondiente a
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>B</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{B}</annotation>
            </semantics>
          </math>
          estará ubicado sobre la diagonal, cerca de la esquina inferior
          izquierda. El punto correspondiente a
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>F</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{F}</annotation>
            </semantics>
          </math>
          estará ubicado sobre la diagonal, en un lugar intermedio. Finalmente, el
          punto correspondiente a
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{D}</annotation>
            </semantics>
          </math>
          estará ubicado en la diagonal, cerca de la esquina superior derecha.
        </p>
        <div class="d-flex justify-center">
          <v-img src="../assets/grafico1.png" class="v-col-md-3 v-col-sm-6"/>
        </div>
        <h2>Línea de alimentación.</h2>
        <p>La variable q representa el estado térmico de la alimentación. De
          esta forma:</p>
        <p>Alimentación como líquido subenfriado,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>&gt;</mo>
                <mn>1</mn>
              </mrow>
              <annotation encoding="application/x-tex">q &gt; 1</annotation>
            </semantics>
          </math>
        </p>
        <p>Alimentación como líquido saturado,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>=</mo>
                <mn>1</mn>
              </mrow>
              <annotation encoding="application/x-tex">q = 1</annotation>
            </semantics>
          </math>
        </p>
        <p>Alimentación como mezcla de vapor y líquido,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mn>0</mn>
                <mo>&lt;</mo>
                <mi>q</mi>
                <mo>&lt;</mo>
                <mn>1</mn>
              </mrow>
              <annotation encoding="application/x-tex">0 &lt; q &lt; 1</annotation>
            </semantics>
          </math>
        </p>
        <p>Alimentación como vapor saturado,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>=</mo>
                <mn>0</mn>
              </mrow>
              <annotation encoding="application/x-tex">q = 0</annotation>
            </semantics>
          </math>
        </p>
        <p>Alimentación como vapor sobrecalentado,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>&lt;</mo>
                <mn>0</mn>
              </mrow>
              <annotation encoding="application/x-tex">q &lt; 0</annotation>
            </semantics>
          </math>
        </p>
        <p>El programa no calcula el valor de q, pues se espera que sea
          proporcionado por el usuario. El cálculo de q debe efectuarse
          manualmente, pudiendo efectuarse con alguna de las siguientes
          ecuaciones:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>=</mo>
                <mn>1</mn>
                <mo>+</mo>
                <mfrac>
                  <mrow>
                    <msub>
                      <mi>C</mi>
                      <mrow>
                        <mi>p</mi>
                        <mi>L</mi>
                      </mrow>
                    </msub>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <msub>
                        <mi>T</mi>
                        <mi>b</mi>
                      </msub>
                      <mo>−</mo>
                      <msub>
                        <mi>T</mi>
                        <mi>F</mi>
                      </msub>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                  </mrow>
                  <mi>λ</mi>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">q = 1 + \frac{C_{pL}(T_{b} - T_{F})}{\lambda}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>q</mi>
                <mo>=</mo>
                <mi>−</mi>
                <mfrac>
                  <mrow>
                    <msub>
                      <mi>C</mi>
                      <mrow>
                        <mi>p</mi>
                        <mi>V</mi>
                      </mrow>
                    </msub>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <msub>
                        <mi>T</mi>
                        <mi>F</mi>
                      </msub>
                      <mo>−</mo>
                      <msub>
                        <mi>T</mi>
                        <mi>d</mi>
                      </msub>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                  </mrow>
                  <mi>λ</mi>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">q = - \frac{C_{pV}(T_{F} - T_{d})}{\lambda}</annotation>
            </semantics>
          </math>
        </p>
        <p>Donde:</p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>c</mi>
                  <mrow>
                    <mi>p</mi>
                    <mi>L</mi>
                  </mrow>
                </msub>
                <mo>,</mo>
                <mspace width="0.222em"></mspace>
                <msub>
                  <mi>c</mi>
                  <mrow>
                    <mi>p</mi>
                    <mi>V</mi>
                  </mrow>
                </msub>
              </mrow>
              <annotation encoding="application/x-tex">c_{pL},\ c_{pV}</annotation>
            </semantics>
          </math>
          = calores específicos del líquido y el vapor, respectivamente
        </p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>T</mi>
                <mi>F</mi>
              </msub>
              <annotation encoding="application/x-tex">T_{F}</annotation>
            </semantics>
          </math>
          = temperatura de la alimentación
        </p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>T</mi>
                  <mi>b</mi>
                </msub>
                <mo>,</mo>
                <mspace width="0.222em"></mspace>
                <msub>
                  <mi>T</mi>
                  <mi>d</mi>
                </msub>
              </mrow>
              <annotation encoding="application/x-tex">T_{b},\ T_{d}</annotation>
            </semantics>
          </math>
          = temperaturas del punto de burbuja y del punto de rocío de la
          alimentación, respectivamente
        </p>
        <p>
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>λ</mi>
              <annotation encoding="application/x-tex">\lambda</annotation>
            </semantics>
          </math>
          = calor de vaporización
        </p>
        <p>Con el valor de q, se traza la línea de alimentación, la cual está
          representada por:</p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th>
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <mi>y</mi>
                    <mo>=</mo>
                    <mi>−</mi>
                    <mfrac>
                      <mi>q</mi>
                      <mrow>
                        <mn>1</mn>
                        <mo>−</mo>
                        <mi>q</mi>
                      </mrow>
                    </mfrac>
                    <mi>x</mi>
                    <mo>+</mo>
                    <mfrac>
                      <msub>
                        <mi>x</mi>
                        <mi>F</mi>
                      </msub>
                      <mrow>
                        <mn>1</mn>
                        <mo>−</mo>
                        <mi>q</mi>
                      </mrow>
                    </mfrac>
                  </mrow>
                  <annotation encoding="application/x-tex">y = - \frac{q}{1 - q}x + \frac{x_{F}}{1 - q}</annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 3)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <p>El punto en el que se intersecta la línea de alimentación y la curva
          de equilibrio corresponde a las coordenadas
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>x</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">x&#39;</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>y</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">y&#39;</annotation>
            </semantics>
          </math>
          ).
          Hallar esas coordenadas es muy sencillo si nos basamos en un método
          gráfico, pero si deseamos encontrar las coordenadas de forma algebraica,
          se hace necesario operar la ecuación 1 y la ecuación 3.
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mfrac>
                  <mrow>
                    <mi>α</mi>
                    <mi>x</mi>
                  </mrow>
                  <mrow>
                    <mn>1</mn>
                    <mo>+</mo>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <mi>α</mi>
                      <mo>−</mo>
                      <mn>1</mn>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                    <mi>x</mi>
                  </mrow>
                </mfrac>
                <mo>=</mo>
                <mi>−</mi>
                <mfrac>
                  <mi>q</mi>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
                <mi>x</mi>
                <mo>+</mo>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>F</mi>
                  </msub>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">\frac{\alpha x}{1 + (\alpha - 1)x} = - \frac{q}{1 - q}x +
                \frac{x_{F}}{1 - q}
              </annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mrow>
                  <mo stretchy="true" form="prefix">[</mo>
                  <mfrac>
                    <mrow>
                      <mi>q</mi>
                      <mrow>
                        <mo stretchy="true" form="prefix">(</mo>
                        <mi>α</mi>
                        <mo>−</mo>
                        <mn>1</mn>
                        <mo stretchy="true" form="postfix">)</mo>
                      </mrow>
                    </mrow>
                    <mrow>
                      <mn>1</mn>
                      <mo>−</mo>
                      <mi>q</mi>
                    </mrow>
                  </mfrac>
                  <mo stretchy="true" form="postfix">]</mo>
                </mrow>
                <msup>
                  <mi>x</mi>
                  <mn>2</mn>
                </msup>
                <mo>+</mo>
                <mrow>
                  <mo stretchy="true" form="prefix">[</mo>
                  <mi>α</mi>
                  <mo>+</mo>
                  <mfrac>
                    <mrow>
                      <mi>q</mi>
                      <mo>−</mo>
                      <msub>
                        <mi>x</mi>
                        <mi>F</mi>
                      </msub>
                      <mrow>
                        <mo stretchy="true" form="prefix">(</mo>
                        <mi>α</mi>
                        <mo>−</mo>
                        <mn>1</mn>
                        <mo stretchy="true" form="postfix">)</mo>
                      </mrow>
                    </mrow>
                    <mrow>
                      <mn>1</mn>
                      <mo>−</mo>
                      <mi>q</mi>
                    </mrow>
                  </mfrac>
                  <mo stretchy="true" form="postfix">]</mo>
                </mrow>
                <mi>x</mi>
                <mo>−</mo>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>F</mi>
                  </msub>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
                <mo>=</mo>
                <mn>0</mn>
              </mrow>
              <annotation encoding="application/x-tex">\left\lbrack \frac{q(\alpha - 1)}{1 - q} \right\rbrack x^{2} +
                \left\lbrack \alpha + \frac{q - x_{F}(\alpha - 1)}{1 - q} \right\rbrack x - \frac{x_{F}}{1 - q} = 0
              </annotation>
            </semantics>
          </math>
        </p>
        <p>Como se trata de una ecuación de segundo grado, se resuelve mediante
          la fórmula cuadrática:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>x</mi>
                <mo>=</mo>
                <mfrac>
                  <mrow>
                    <mi>−</mi>
                    <mi>b</mi>
                    <mo>±</mo>
                    <msqrt>
                      <mrow>
                        <msup>
                          <mi>b</mi>
                          <mn>2</mn>
                        </msup>
                        <mo>−</mo>
                        <mn>4</mn>
                        <mi>a</mi>
                        <mi>c</mi>
                      </mrow>
                    </msqrt>
                  </mrow>
                  <mrow>
                    <mn>2</mn>
                    <mi>a</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">x = \frac{- b \pm \sqrt{b^{2} - 4ac}}{2a}</annotation>
            </semantics>
          </math>
        </p>
        <p>En donde:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>a</mi>
                <mo>=</mo>
                <mfrac>
                  <mrow>
                    <mi>q</mi>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <mi>α</mi>
                      <mo>−</mo>
                      <mn>1</mn>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                  </mrow>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">a = \frac{q(\alpha - 1)}{1 - q}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>b</mi>
                <mo>=</mo>
                <mi>α</mi>
                <mo>+</mo>
                <mfrac>
                  <mrow>
                    <mi>q</mi>
                    <mo>−</mo>
                    <msub>
                      <mi>x</mi>
                      <mi>F</mi>
                    </msub>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <mi>α</mi>
                      <mo>−</mo>
                      <mn>1</mn>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                  </mrow>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">b = \alpha + \frac{q - x_{F}(\alpha - 1)}{1 - q}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>c</mi>
                <mo>=</mo>
                <mi>−</mi>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>F</mi>
                  </msub>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">c = - \frac{x_{F}}{1 - q}</annotation>
            </semantics>
          </math>
        </p>
        <p>La raíz (solución) positiva debe asignarse a
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>x</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">x&#39;</annotation>
            </semantics>
          </math>
          .
          La raíz negativa se desecha y no toma parte ulterior en los cálculos.
          Por otra parte,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>y</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">y&#39;</annotation>
            </semantics>
          </math>
          se obtiene reemplazando
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>x</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">x&#39;</annotation>
            </semantics>
          </math>
          en la ecuación 1.
        </p>
        <h2>Línea de rectificación.</h2>
        <p>Se representa mediante la ecuación:</p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th>
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <mi>y</mi>
                    <mo>=</mo>
                    <mspace width="0.222em"></mspace>
                    <mfrac>
                      <msub>
                        <mi>R</mi>
                        <mi>D</mi>
                      </msub>
                      <mrow>
                        <msub>
                          <mi>R</mi>
                          <mi>D</mi>
                        </msub>
                        <mo>+</mo>
                        <mn>1</mn>
                      </mrow>
                    </mfrac>
                    <mi>x</mi>
                    <mo>+</mo>
                    <mfrac>
                      <msub>
                        <mi>x</mi>
                        <mi>D</mi>
                      </msub>
                      <mrow>
                        <msub>
                          <mi>R</mi>
                          <mi>D</mi>
                        </msub>
                        <mo>+</mo>
                        <mn>1</mn>
                      </mrow>
                    </mfrac>
                  </mrow>
                  <annotation encoding="application/x-tex">y = \ \frac{R_{D}}{R_{D} + 1}x + \frac{x_{D}}{R_{D} + 1}
                  </annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 4)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <h2>Reflujo.</h2>
        <p>El reflujo se refiere a un corriente de destilado condensado que
          retorna a la torre de destilación, se representa con la letra
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>L</mi>
              <annotation encoding="application/x-tex">L</annotation>
            </semantics>
          </math>
          .
          La corriente del destilado o producto se representa con la letra
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>D</mi>
              <annotation encoding="application/x-tex">D</annotation>
            </semantics>
          </math>
          .
          La relación de reflujo, es el cociente entre ambas corrientes, es
          decir:
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>R</mi>
                  <mi>D</mi>
                </msub>
                <mo>=</mo>
                <mfrac>
                  <mi>L</mi>
                  <mi>D</mi>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">R_{D} = \frac{L}{D}</annotation>
            </semantics>
          </math>
        </p>
        <p>Si la relación de reflujo es infinita
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>D</mi>
                <mo>=</mo>
                <mn>0</mn>
              </mrow>
              <annotation encoding="application/x-tex">D = 0</annotation>
            </semantics>
          </math>
          ),
          el número de platos requeridos es mínimo pero no cero. A esto se
          denomina reflujo total, pues el destilado no se extrae.
        </p>
        <p>Existe también el concepto de relación de reflujo mínima
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mrow>
                  <mi>D</mi>
                  <mi>m</mi>
                  <mi>i</mi>
                  <mi>n</mi>
                </mrow>
              </msub>
              <annotation encoding="application/x-tex">R_{Dmin}</annotation>
            </semantics>
          </math>
          ),
          el cual es el valor más bajo que permite lograr la separación deseada en
          una columna de destilación, pero con un número de platos infinito.
        </p>
        <p>Hallar el valor de
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mrow>
                  <mi>D</mi>
                  <mi>m</mi>
                  <mi>i</mi>
                  <mi>n</mi>
                </mrow>
              </msub>
              <annotation encoding="application/x-tex">R_{Dmin}</annotation>
            </semantics>
          </math>
          es relativamente sencillo cuando se realiza de forma gráfica, pues basta
          con trazar una recta desde el punto
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{D}</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>y</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">y_{D}</annotation>
            </semantics>
          </math>
          )
          pasando por el punto
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>x</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">x&#39;</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>y</mi>
                <mi>′</mi>
              </mrow>
              <annotation encoding="application/x-tex">y&#39;</annotation>
            </semantics>
          </math>
          ),
          hasta intersectar el eje
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>y</mi>
              <annotation encoding="application/x-tex">y</annotation>
            </semantics>
          </math>
          .
          La ordenada en el origen representa el valor de
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mfrac>
                <msub>
                  <mi>x</mi>
                  <mrow>
                    <mi>D</mi>
                  </mrow>
                </msub>
                <mrow>
                  <msub>
                    <mi>R</mi>
                    <mrow>
                      <mi>D</mi>
                      <mi>m</mi>
                      <mi>i</mi>
                      <mi>n</mi>
                    </mrow>
                  </msub>
                  <mo>+</mo>
                  <mn>1</mn>
                </mrow>
              </mfrac>
              <annotation encoding="application/x-tex">\frac{R_{Dmin}}{R_{Dmin} + 1}</annotation>
            </semantics>
          </math>
        </p>
        <div class="d-flex justify-center">
          <v-img src="../assets/grafico2.png" class="v-col-md-4 v-col-sm-6"/>
        </div>
        <p>Para hallar
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mrow>
                  <mi>D</mi>
                  <mi>m</mi>
                  <mi>i</mi>
                  <mi>n</mi>
                </mrow>
              </msub>
              <annotation encoding="application/x-tex">R_{Dmin}</annotation>
            </semantics>
          </math>
          de forma algebraica, se puede emplear la siguiente ecuación:
        </p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th>
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <msub>
                      <mi>R</mi>
                      <mrow>
                        <mi>D</mi>
                        <mi>m</mi>
                        <mi>i</mi>
                        <mi>n</mi>
                      </mrow>
                    </msub>
                    <mo>=</mo>
                    <mfrac>
                      <mrow>
                        <msub>
                          <mi>x</mi>
                          <mi>D</mi>
                        </msub>
                        <mrow>
                          <mo stretchy="true" form="prefix">(</mo>
                          <msub>
                            <mi>x</mi>
                            <mi>D</mi>
                          </msub>
                          <mo>−</mo>
                          <msup>
                            <mi>x</mi>
                            <mi>′</mi>
                          </msup>
                          <mo stretchy="true" form="postfix">)</mo>
                        </mrow>
                      </mrow>
                      <mrow>
                        <msub>
                          <mi>x</mi>
                          <mi>D</mi>
                        </msub>
                        <msup>
                          <mi>y</mi>
                          <mi>′</mi>
                        </msup>
                        <mo>−</mo>
                        <mi>x</mi>
                        <mi>′</mi>
                        <msub>
                          <mi>x</mi>
                          <mi>D</mi>
                        </msub>
                      </mrow>
                    </mfrac>
                    <mo>−</mo>
                    <mn>1</mn>
                  </mrow>
                  <annotation encoding="application/x-tex">R_{Dmin} = \frac{x_{D}(x_{D} - x^{&#39;})}{x_{D}y^{&#39;} - x&#39;x_{D}}
                    - 1
                  </annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 5)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <p>La forma en la que se logró obtener la ecuación 5 no se demostrará en
          extenso, pero se parte de un sistema de ecuaciones conformado por:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mrow>
                  <mo stretchy="true" form="prefix">{</mo>
                  <mtable>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <mi>y</mi>
                        <mo>=</mo>
                        <mfrac>
                          <mrow>
                            <msub>
                              <mi>y</mi>
                              <mi>D</mi>
                            </msub>
                            <mo>−</mo>
                            <mi>y</mi>
                            <mi>′</mi>
                          </mrow>
                          <mrow>
                            <msub>
                              <mi>x</mi>
                              <mi>D</mi>
                            </msub>
                            <mo>−</mo>
                            <mi>x</mi>
                            <mi>′</mi>
                          </mrow>
                        </mfrac>
                        <mo>+</mo>
                        <msup>
                          <mi>y</mi>
                          <mi>′</mi>
                        </msup>
                        <mo>,</mo>
                        <mspace width="0.222em"></mspace>
                        <mi>a</mi>
                        <mi>d</mi>
                        <mi>e</mi>
                        <mi>m</mi>
                        <mi>á</mi>
                        <mi>s</mi>
                        <mspace width="0.222em"></mspace>
                        <msub>
                          <mi>x</mi>
                          <mi>D</mi>
                        </msub>
                        <mo>=</mo>
                        <msub>
                          <mi>y</mi>
                          <mi>D</mi>
                        </msub>
                      </mtd>
                    </mtr>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <mi>y</mi>
                        <mo>=</mo>
                        <mspace width="0.222em"></mspace>
                        <mfrac>
                          <msub>
                            <mi>x</mi>
                            <mi>D</mi>
                          </msub>
                          <mrow>
                            <msub>
                              <mi>R</mi>
                              <mrow>
                                <mi>D</mi>
                                <mi>m</mi>
                                <mi>i</mi>
                                <mi>n</mi>
                              </mrow>
                            </msub>
                            <mo>+</mo>
                            <mn>1</mn>
                          </mrow>
                        </mfrac>
                      </mtd>
                    </mtr>
                  </mtable>
                </mrow>
                <mspace width="0.222em"></mspace>
              </mrow>
              <annotation encoding="application/x-tex">\left\{ \begin{array}{r}
                y = \frac{y_{D} - y&#39;}{x_{D} - x&#39;} + y^{&#39;},\ además\ x_{D} = y_{D} \\
                y = \ \frac{x_{D}}{R_{Dmin} + 1}
                \end{array} \right.\
              </annotation>
            </semantics>
          </math>
        </p>
        <p>En la práctica, el valor de la relación de reflujo
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">R_{D}</annotation>
            </semantics>
          </math>
          )
          generalmente se toma como un múltiplo del reflujo mínimo
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mrow>
                  <mi>D</mi>
                  <mi>m</mi>
                  <mi>i</mi>
                  <mi>n</mi>
                </mrow>
              </msub>
              <annotation encoding="application/x-tex">R_{Dmin}</annotation>
            </semantics>
          </math>
          )
          para equilibrar la eficiencia de separación y los costos energéticos de
          operación. Un valor intermedio de 1.3 veces el valor de
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mrow>
                  <mi>D</mi>
                  <mi>m</mi>
                  <mi>i</mi>
                  <mi>n</mi>
                </mrow>
              </msub>
              <annotation encoding="application/x-tex">R_{Dmin}</annotation>
            </semantics>
          </math>
          es comúnmente aceptado como un factor de operación razonable. A ese
          factor se lo denomina como factor de reflujo, y en el presente análisis
          se simboliza con la letra
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mi>f</mi>
              <annotation encoding="application/x-tex">f</annotation>
            </semantics>
          </math>
          .
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>R</mi>
                  <mi>D</mi>
                </msub>
                <mo>=</mo>
                <mi>f</mi>
                <mo>•</mo>
                <msub>
                  <mi>R</mi>
                  <mrow>
                    <mi>D</mi>
                    <mi>m</mi>
                    <mi>i</mi>
                    <mi>n</mi>
                  </mrow>
                </msub>
              </mrow>
              <annotation encoding="application/x-tex">R_{D} = f \bullet R_{Dmin}</annotation>
            </semantics>
          </math>
        </p>
        <p>El programa solicita el factor de reflujo como una de las entradas
          necesarias para su funcionamiento.</p>
        <p>Una vez calculado el valor de
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>R</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">R_{D}</annotation>
            </semantics>
          </math>
          ,
          se traza una línea que parte de
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{D}</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>y</mi>
                <mi>D</mi>
              </msub>
              <annotation encoding="application/x-tex">y_{D}</annotation>
            </semantics>
          </math>
          )
          y pasa por el punto (0,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mspace width="0.222em"></mspace>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>D</mi>
                  </msub>
                  <mrow>
                    <msub>
                      <mi>R</mi>
                      <mi>D</mi>
                    </msub>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">\ \frac{x_{D}}{R_{D} + 1}</annotation>
            </semantics>
          </math>
          ).
          Esta línea intersecta a la línea de alimentación en un punto, en el
          programa, denominado con las variables
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mn>2</mn>
              </msub>
              <annotation encoding="application/x-tex">x_{2}</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>y</mi>
                <mn>2</mn>
              </msub>
              <annotation encoding="application/x-tex">y_{2}</annotation>
            </semantics>
          </math>
          ).
        </p>
        <p>Para hallar este punto de forma algebraica se resuelve un sistema de
          ecuaciones compuesto por la ecuación 3 y la ecuación 4:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mrow>
                  <mo stretchy="true" form="prefix">{</mo>
                  <mtable>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <msub>
                          <mi>y</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>=</mo>
                        <mi>−</mi>
                        <mfrac>
                          <mi>q</mi>
                          <mrow>
                            <mn>1</mn>
                            <mo>−</mo>
                            <mi>q</mi>
                          </mrow>
                        </mfrac>
                        <msub>
                          <mi>x</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>+</mo>
                        <mfrac>
                          <msub>
                            <mi>x</mi>
                            <mi>F</mi>
                          </msub>
                          <mrow>
                            <mn>1</mn>
                            <mo>−</mo>
                            <mi>q</mi>
                          </mrow>
                        </mfrac>
                      </mtd>
                    </mtr>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <msub>
                          <mi>y</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>=</mo>
                        <mspace width="0.222em"></mspace>
                        <mfrac>
                          <msub>
                            <mi>R</mi>
                            <mi>D</mi>
                          </msub>
                          <mrow>
                            <msub>
                              <mi>R</mi>
                              <mi>D</mi>
                            </msub>
                            <mo>+</mo>
                            <mn>1</mn>
                          </mrow>
                        </mfrac>
                        <msub>
                          <mi>x</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>+</mo>
                        <mfrac>
                          <msub>
                            <mi>x</mi>
                            <mi>D</mi>
                          </msub>
                          <mrow>
                            <msub>
                              <mi>R</mi>
                              <mi>D</mi>
                            </msub>
                            <mo>+</mo>
                            <mn>1</mn>
                          </mrow>
                        </mfrac>
                      </mtd>
                    </mtr>
                  </mtable>
                </mrow>
                <mspace width="0.222em"></mspace>
              </mrow>
              <annotation encoding="application/x-tex">\left\{ \begin{array}{r}
                y_{2} = - \frac{q}{1 - q}x_{2} + \frac{x_{F}}{1 - q} \\
                y_{2} = \ \frac{R_{D}}{R_{D} + 1}x_{2} + \frac{x_{D}}{R_{D} + 1}
                \end{array} \right.\
              </annotation>
            </semantics>
          </math>
        </p>
        <p>Se realiza un cambio de variables:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>a</mi>
                <mo>=</mo>
                <mi>−</mi>
                <mfrac>
                  <mi>q</mi>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">a = - \frac{q}{1 - q}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>b</mi>
                <mo>=</mo>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>F</mi>
                  </msub>
                  <mrow>
                    <mn>1</mn>
                    <mo>−</mo>
                    <mi>q</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">b = \frac{x_{F}}{1 - q}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>c</mi>
                <mo>=</mo>
                <mfrac>
                  <msub>
                    <mi>R</mi>
                    <mi>D</mi>
                  </msub>
                  <mrow>
                    <msub>
                      <mi>R</mi>
                      <mi>D</mi>
                    </msub>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">c = \frac{R_{D}}{R_{D} + 1}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mi>d</mi>
                <mo>=</mo>
                <mfrac>
                  <msub>
                    <mi>x</mi>
                    <mi>D</mi>
                  </msub>
                  <mrow>
                    <msub>
                      <mi>R</mi>
                      <mi>D</mi>
                    </msub>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">d = \frac{x_{D}}{R_{D} + 1}</annotation>
            </semantics>
          </math>
        </p>
        <p>De esta forma, el sistema de ecuaciones se convierte en:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <mrow>
                  <mo stretchy="true" form="prefix">{</mo>
                  <mtable>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <msub>
                          <mi>y</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>=</mo>
                        <mi>a</mi>
                        <msub>
                          <mi>x</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>+</mo>
                        <mi>b</mi>
                      </mtd>
                    </mtr>
                    <mtr>
                      <mtd columnalign="right" style="text-align: right">
                        <msub>
                          <mi>y</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>=</mo>
                        <mspace width="0.222em"></mspace>
                        <mi>c</mi>
                        <msub>
                          <mi>x</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>+</mo>
                        <mi>d</mi>
                      </mtd>
                    </mtr>
                  </mtable>
                </mrow>
                <mspace width="0.222em"></mspace>
              </mrow>
              <annotation encoding="application/x-tex">\left\{ \begin{array}{r}
                y_{2} = ax_{2} + b \\
                y_{2} = \ cx_{2} + d
                \end{array} \right.\
              </annotation>
            </semantics>
          </math>
        </p>
        <p>La solución es:</p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>x</mi>
                  <mn>2</mn>
                </msub>
                <mo>=</mo>
                <mfrac>
                  <mrow>
                    <mi>d</mi>
                    <mo>−</mo>
                    <mi>b</mi>
                  </mrow>
                  <mrow>
                    <mi>a</mi>
                    <mo>−</mo>
                    <mi>c</mi>
                  </mrow>
                </mfrac>
              </mrow>
              <annotation encoding="application/x-tex">x_{2} = \frac{d - b}{a - c}</annotation>
            </semantics>
          </math>
        </p>
        <p>
          <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <mrow>
                <msub>
                  <mi>y</mi>
                  <mn>2</mn>
                </msub>
                <mo>=</mo>
                <mi>a</mi>
                <msub>
                  <mi>x</mi>
                  <mn>2</mn>
                </msub>
                <mo>+</mo>
                <mi>b</mi>
              </mrow>
              <annotation encoding="application/x-tex">y_{2} = ax_{2} + b</annotation>
            </semantics>
          </math>
        </p>
        <h2>Línea de agotamiento.</h2>
        <p>La línea de agotamiento es una línea que empieza en
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>B</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{B}</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>y</mi>
                <mi>B</mi>
              </msub>
              <annotation encoding="application/x-tex">y_{B}</annotation>
            </semantics>
          </math>
          )
          y termina en
          (
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mn>2</mn>
              </msub>
              <annotation encoding="application/x-tex">x_{2}</annotation>
            </semantics>
          </math>
          ,
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>y</mi>
                <mn>2</mn>
              </msub>
              <annotation encoding="application/x-tex">y_{2}</annotation>
            </semantics>
          </math>
          ).
          En el programa, la línea de agotamiento emplea la siguiente ecuación
          para realizar el escalonado correspondiente a los platos:
        </p>
        <table>
          <colgroup>
            <col style="width: 50%"/>
            <col style="width: 50%"/>
          </colgroup>
          <thead>
          <tr>
            <th>
              <math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
                <semantics>
                  <mrow>
                    <mi>y</mi>
                    <mo>=</mo>
                    <mfrac>
                      <mrow>
                        <msub>
                          <mi>y</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>−</mo>
                        <msub>
                          <mi>x</mi>
                          <mi>B</mi>
                        </msub>
                      </mrow>
                      <mrow>
                        <msub>
                          <mi>x</mi>
                          <mn>2</mn>
                        </msub>
                        <mo>−</mo>
                        <msub>
                          <mi>x</mi>
                          <mi>B</mi>
                        </msub>
                      </mrow>
                    </mfrac>
                    <mrow>
                      <mo stretchy="true" form="prefix">(</mo>
                      <mi>x</mi>
                      <mo>−</mo>
                      <msub>
                        <mi>x</mi>
                        <mi>B</mi>
                      </msub>
                      <mo stretchy="true" form="postfix">)</mo>
                    </mrow>
                    <mo>+</mo>
                    <msub>
                      <mi>x</mi>
                      <mi>B</mi>
                    </msub>
                  </mrow>
                  <annotation encoding="application/x-tex">y = \frac{y_{2} - x_{B}}{x_{2} - x_{B}}\left( x - x_{B}
                    \right) + x_{B}
                  </annotation>
                </semantics>
              </math>
            </th>
            <th>(Ec. 6)</th>
          </tr>
          </thead>
          <tbody>
          </tbody>
        </table>
        <h2>Escalonado.</h2>
        <p>Finalmente queda efectuar el proceso de escalonado, es decir, el
          proceso de construir "escalones", "gradas", intersectando de manera
          sucesiva, con líneas verticales y horizontales, la curva de equilibrio y
          la línea de rectificación (o la línea de agotamiento, si corresponde).
          Cada escalón representa un plato de la columna de destilación y el
          escalón que se sobrepone a la línea de alimentación corresponde al plato
          de alimentación. El proceso de crear escalones se realiza de tal forma
          que el último escalón sea menor o igual que
          <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML">
            <semantics>
              <msub>
                <mi>x</mi>
                <mi>B</mi>
              </msub>
              <annotation encoding="application/x-tex">x_{B}</annotation>
            </semantics>
          </math>
          .
        </p>
        <div class="d-flex justify-center">
          <v-img src="../assets/grafico3.png" class="v-col-md-4 v-col-sm-6" />
        </div>
        <h2>Bibliografía.</h2>
        <p>McCabe, W. L., Smith, J. C., y Harriott, P. (2007). OPERACIONES
          UNITARIAS EN INGENIERÍA QUÍMICA (séptima edición). Editorial
          McGraw-Hill. México D.F., México.</p>


      </v-card-text>
    </v-card>
  </v-container>
</template>
<script>

</script>
<style>
p {
  margin-top: 10px;
  margin-bottom: 10px;
  text-align: justify;
}

table {
  width: 100%;
}
</style>
