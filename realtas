import imoveis from "../imoveis.json" assert { type: "json" };

export default function handler(req, res) {
  const query = req.query; // pega todos os parâmetros da URL
  let resultado = imoveis;

  resultado = resultado.filter(item => {
    for (let key in query) {
      const valorQuery = query[key].toLowerCase();
      const valorItem = item[key];

      if (valorItem === undefined) return false;

      // Se for array (ex.: caracteristicas)
      if (Array.isArray(valorItem)) {
        const match = valorItem.some(v => v.toString().toLowerCase() === valorQuery);
        if (!match) return false;
      }
      // Se for número
      else if (typeof valorItem === "number") {
        if (!isNaN(valorQuery)) {
          if (valorItem !== parseFloat(valorQuery)) return false;
        } else {
          return false; // query inválida para número
        }
      }
      // Se for string
      else if (typeof valorItem === "string") {
        if (!valorItem.toLowerCase().includes(valorQuery)) return false; // busca parcial
      }
      // Outros tipos podem ser ignorados ou tratados aqui
      else {
        if (valorItem.toString().toLowerCase() !== valorQuery) return false;
      }
    }
    return true;
  });

  res.status(200).json(resultado);
}
