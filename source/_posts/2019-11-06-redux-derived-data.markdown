---
layout: post
title: "[Redux] Derived data"
date: 2019-11-06 13:50:30 -0300
comments: true
categories: [redux]
---
Reducer:

~~~javascript 
const emprestimo = (
  state = {
    numeroMeses: new BigNumber(36),
    taxa: new BigNumber(1.82),
    valorPrestacao: new BigNumber(304),
    valorFinanciado: new BigNumber(10000)
  },
  action
) => {
  switch (action.type) {
    case "NUMERO_MESES":
      return { ...state, numeroMeses: action.numeroMeses };
    case "TAXA":
      return { ...state, taxa: action.taxa };
    case "VALOR_PRESTACAO":
      return { ...state, valorPrestacao: action.valorPrestacao };
    case "VALOR_FINANCIADO":
      return { ...state, valorFinanciado: action.valorFinanciado };
    default:
      return state;
  }
};
~~~

How to calculate the result values?

Create a selector, using reselect!

~~~javascript

const valores = state => state;

const derivados = createSelector(valores, state => {
  ///calculate the total...

  return {
    total: total
  };
});

~~~

With the `selector` we need to conect with the `reducers`:

~~~javascript

const mapStateToProps = state => {
  return {
    derivados: derivados(state)
  };
};

connect(mapStateToProps)(CalculoPrestacao);

~~~

To use, just do the normal things:

~~~javascript
const {    
    derivados
} = state;
  
<CalculoPrestacao derivados={derivados} />
  
<Resultado derivados={this.props.derivados} />
  
~~~


~~~javascript
const { createSelector } = Reselect;
const { connect } = ReactRedux;
~~~

[Documentação](https://redux.js.org/recipes/computing-derived-data)