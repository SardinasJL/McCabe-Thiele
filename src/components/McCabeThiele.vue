<template>
  <div class="text-center">
    <div id="plot" ref="plotContainer"></div>
    <v-btn @click="descargarGrafico">Descargar Gráfico</v-btn>
  </div>
</template>

<script>
import functionPlot from "function-plot";

export default {
  name: "McCabeThiele",
  props: {
    alfa: {
      type: Number,
      required: true,
    },
    xF: {
      type: Number,
      required: true,
    },
    xD: {
      type: Number,
      required: true,
    },
    xB: {
      type: Number,
      required: true,
    },
    q: {
      type: Number,
      required: true,
    },
    f: {
      type: Number,
      required: true,
    },
  },
  methods: {
    curvaDeEquilibrio(x, alfa) {
      return (alfa * x) / (1 + x * (alfa - 1));
    },
    curvaDeEquilibrioInv(y, alfa) {
      return -y / (y * (alfa - 1) - alfa);
    },
    formulaCuadratica(a, b, c) {
      const discriminante = Math.pow(b, 2) - 4 * a * c;
      if (discriminante > 0) {
        return [
          (-b + Math.sqrt(discriminante)) / (2 * a),
          (-b - Math.sqrt(discriminante)) / (2 * a),
        ];
      } else if (discriminante === 0) {
        const x = -b / (2 * a);
        return [x, x];
      } else {
        return [
          `${-b / (2 * a)} + ${Math.sqrt(-discriminante) / (2 * a)}i`,
          `${-b / (2 * a)} - ${Math.sqrt(-discriminante) / (2 * a)}i`,
        ];
      }
    },
    sistemaDeEcuaciones2x2(a, b, c, d) {
      const x = (d - b) / (a - c);
      const y = a * x + b;
      return [x, y];
    },
    xPrimayPrima(q, xF, alfa) {//xPrimayPrima = intersección de la línea de alimentación con la curva de equilibrio
      if (q == 1)//caso especial, si q es igual a 1
        return [xF, this.curvaDeEquilibrio(xF, alfa)];
      if (q == 0)
        return [this.curvaDeEquilibrioInv(xF, alfa), xF];
      let a = (q * (alfa - 1)) / (1 - q);
      let b = alfa + (q - xF * (alfa - 1)) / (1 - q);
      let c = -(xF) / (1 - q);
      let raices = this.formulaCuadratica(a, b, c);
      if (typeof raices[0] !== 'number' || typeof raices[1] !== 'number')
        throw new Error("Hubo un error");
      let xPrima;
      if (raices[0] > 0)//se toma únicamente la raíz positiva
        xPrima = raices[0];
      else
        xPrima = raices[1];
      let yPrima = this.curvaDeEquilibrio(xPrima, alfa);
      return [xPrima, yPrima];
    },
    RDm(xD, xPrima, yPrima) {
      return ((xD * (xD - xPrima)) / (xD * yPrima - xPrima * xD)) - 1;
    },
    x2y2(RD, xD, q, xF) {//x2y2 son las coordendas en donde se intersecta la línea de alimentación con la LOZR
      if (q == 1) //Caso especial, si q es 1, la línea es una línea vertical
        return [xF, ((RD * xF) / (RD + 1)) + (xD / (RD + 1))];
      let a = RD / (RD + 1);
      let b = xD / (RD + 1);
      let c = -q / (1 - q);
      let d = xF / (1 - q);
      return this.sistemaDeEcuaciones2x2(a, b, c, d);
    },
    calcularEscalones(alfa, xB, xF, xD, x2, y2, q, f, RD) {
      let x0 = xD, y0 = xD, x1, y1;
      let puntosDeLosEscalones = [], cantidadDePlatos = 0;
      while (x0 > xB) {
        y1 = y0;
        x1 = -y1 / (y1 * (alfa - 1) - alfa);
        puntosDeLosEscalones.push([x0, y0], [x1, y1]);
        x0 = x1;
        if (x0 > x2)
          y0 = ((RD * x0) / (RD + 1)) + (xD / (RD + 1));
        else
          y0 = (((y2 - xB) * (x0 - xB)) / (x2 - xB)) + xB;
        cantidadDePlatos++;
      }
      puntosDeLosEscalones.push([x0, x0]);
      return {
        puntosDeLosEscalones,
        cantidadDePlatos,
      };
    },
    graficaMcCabeThiele() {
      // Limpia el contenedor del gráfico
      const plotContainer = this.$refs.plotContainer;
      plotContainer.innerHTML = "";

      // Calcula las dimensiones dinámicamente
      const {width} = plotContainer.getBoundingClientRect();
      const height = width; // Mantén proporción 1:1 (ajústalo según necesidad)


      let {alfa, xB, xF, xD, q, f} = this;
      let [xPrima, yPrima] = this.xPrimayPrima(q, xF, alfa);
      let RDmin = this.RDm(xD, xPrima, yPrima);
      let RD = f * RDmin;
      let [x2, y2] = this.x2y2(RD, xD, q, xF);
      let {puntosDeLosEscalones} = this.calcularEscalones(alfa, xB, xF, xD, x2, y2, q, f, RD);

      const puntosImpares = puntosDeLosEscalones.filter((_, index) => index % 2 !== 0);
      //Crea las anotaciones para cada plato, por ejemplo, 1, 2, 3, etc.
      const anotaciones = puntosImpares.map((punto, index) => {
        return {
          text: `${index + 1}`, // Etiqueta del punto
          color: 'black',
          graphType: "text",
          location: [punto[0], punto[1]],
          attr: {
            'text-anchor': 'end'
          }
        };
      });

      //Toma las funciones lineales y los puntos para construir el gráfico
      functionPlot({
        target: '#plot',
        width,
        height,
        xAxis: {domain: [0, 1]},
        yAxis: {domain: [0, 1]},
        disableZoom: true,
        grid: true,
        tip: {
          xLine: true, // dashed line parallel to y = 0
          yLine: true
        },
        data: [
          {
            fn: `${alfa} * x / (1 + x * (${alfa} - 1))`,
            color: '#0d6efd'
          },
          {
            fn: 'x',
            color: '#0d6efd',
          },
          {
            points: [
              [xB, 0],
              [xB, xB]
            ],
            color: 'black',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
            attr: {'stroke-dasharray': '5,5'},
          },
          {
            points: [
              [xF, 0],
              [xF, xF]
            ],
            color: 'black',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
            attr: {'stroke-dasharray': '5,5'},
          },
          {
            points: [
              [xD, 0],
              [xD, xD]
            ],
            color: 'black',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
            attr: {'stroke-dasharray': '5,5'},
          },
          {
            points: [
              [xF, xF],
              [xPrima, yPrima]
            ],
            color: 'black',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
          },
          {
            fn: `((${RDmin} * x) / (${RDmin} + 1)) + (${xD} / (${RDmin} + 1))`,
            color: 'skyblue'
          },
          {
            points: [
              [xD, xD],
              [x2, y2]
            ],
            color: 'green',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
          },
          {
            points: [
              [xB, xB],
              [x2, y2]
            ],
            color: 'green',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
          },
          {
            points: puntosDeLosEscalones,
            color: 'black',
            fnType: 'points',
            graphType: 'polyline', // Dibuja una línea que conecta los puntos
          },
          {
            text: `xB`, // Etiqueta del punto
            color: 'black',
            graphType: "text",
            location: [xB, 0],
            attr: {
              'text-anchor': 'start'
            }
          },
          {
            text: `xF`, // Etiqueta del punto
            color: 'black',
            graphType: "text",
            location: [xF, 0],
            attr: {
              'text-anchor': 'end'
            }
          },
          {
            text: `xD`, // Etiqueta del punto
            color: 'black',
            graphType: "text",
            location: [xD, 0],
            attr: {
              'text-anchor': 'end'
            }
          },
          ...anotaciones
        ],
      });
    },
    handleResize() {
      this.graficaMcCabeThiele(); // Vuelve a generar el gráfico en el cambio de tamaño
    },
    descargarGrafico() {
      const svgElement = this.$refs.plotContainer.querySelector("svg");
      if (!svgElement) {
        alert("No se encontró el gráfico para descargar.");
        return;
      }

      // Clonar el SVG para aplicar estilos específicos de exportación
      const clonedSvg = svgElement.cloneNode(true);

      // Cambiar el tamaño de la fuente en el SVG clonado
      clonedSvg.querySelectorAll("text").forEach((textElement) => {
        textElement.setAttribute("font-size", "12px"); // Tamaño fijo para la exportación
      });

      const svgData = new XMLSerializer().serializeToString(clonedSvg);
      const canvas = document.createElement("canvas");
      const ctx = canvas.getContext("2d");

      // Establecer tamaño deseado (800x800 píxeles)
      const desiredWidth = 800;
      const desiredHeight = 800;
      canvas.width = desiredWidth;
      canvas.height = desiredHeight;

      // Convertir el SVG a una imagen
      const img = new Image();
      const svgBlob = new Blob([svgData], { type: "image/svg+xml;charset=utf-8" });
      const url = URL.createObjectURL(svgBlob);
      img.onload = () => {
        // Escalar y dibujar el SVG en el lienzo
        ctx.drawImage(img, 0, 0, desiredWidth, desiredHeight);
        URL.revokeObjectURL(url); // Liberar memoria

        // Descargar la imagen como PNG
        const link = document.createElement("a");
        link.download = "grafico.png";
        link.href = canvas.toDataURL("image/png");
        link.click();
      };
      img.src = url;
    },
  },
  watch: {
    alfa: "graficaMcCabeThiele",
    xF: "graficaMcCabeThiele",
    xD: "graficaMcCabeThiele",
    xB: "graficaMcCabeThiele",
    q: "graficaMcCabeThiele",
    f: "graficaMcCabeThiele",
  },
  mounted() {
    this.graficaMcCabeThiele();
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  },
};
</script>

<style>
#plot {
  width: 100%;
  height: auto;
}

.function-plot .axis path,
.function-plot .axis line,
.function-plot .tick text {
  font-size: 16px;
}

.function-plot {
  font-size: 16px;
}

@media (max-width: 768px) {
  .function-plot .axis path,
  .function-plot .axis line,
  .function-plot .tick text {
    font-size: 12px; /* Fuente más pequeña en pantallas pequeñas */
  }

  .function-plot {
    font-size: 12px; /* Fuente más pequeña en la gráfica */
  }
}
</style>
