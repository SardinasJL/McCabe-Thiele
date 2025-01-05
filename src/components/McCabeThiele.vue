<template>
  <div>
    <div id="plot"></div>
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
    xPrimayPrima(q, xF, alfa) {
      const a = (q * (alfa - 1)) / (1 - q);
      const b = alfa + (q - xF * (alfa - 1)) / (1 - q);
      const c = -(xF) / (1 - q);
      const [raiz1, raiz2] = this.formulaCuadratica(a, b, c);
      const xPrima = raiz1 > 0 ? raiz1 : raiz2;
      return [xPrima, this.curvaDeEquilibrio(xPrima, alfa)];
    },
    RDm(xD, xPrima, yPrima) {
      return ((xD * (xD - xPrima)) / (xD * yPrima - xPrima * xD)) - 1;
    },
    x2y2(RD, xD, q, xF) {
      const a = RD / (RD + 1);
      const b = xD / (RD + 1);
      const c = -q / (1 - q);
      const d = xF / (1 - q);
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
      const { alfa, xB, xF, xD, q, f } = this;
      const [xPrima, yPrima] = this.xPrimayPrima(q, xF, alfa);
      const RDmin = this.RDm(xD, xPrima, yPrima);
      const RD = f * RDmin;
      const [x2, y2] = this.x2y2(RD, xD, q, xF);
      const { puntosDeLosEscalones } = this.calcularEscalones(
        alfa,
        xB,
        xF,
        xD,
        x2,
        y2,
        q,
        f,
        RD
      );

      functionPlot({
        target: "#plot",
        width: 500,
        height: 500,
        xAxis: { domain: [0, 1] },
        yAxis: { domain: [0, 1] },
        data: [
          { fn: `${alfa} * x / (1 + x * (${alfa} - 1))`, color: "blue" },
          { fn: "x", color: "blue" },
          { points: puntosDeLosEscalones, fnType: "points", graphType: "polyline" },
        ],
      });
    },
  },
  mounted() {
    this.graficaMcCabeThiele();
  },
};
</script>

<style scoped>
.function-plot .axis path,
.function-plot .axis line,
.function-plot .tick text {
  font-size: 16px;
}
.function-plot {
  font-size: 16px;
}
</style>
