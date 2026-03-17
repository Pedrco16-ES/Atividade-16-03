# Atividade-16-03
Solid

interface Trabalhavel {
  trabalhar(): void;
}

interface RegistraPonto {
  registrarPonto(): void;
}

interface Assalariado {
  receberSalario(): void;
}

interface Gerenciavel {
  gerenciarEquipe(): void;
}

interface Programavel {
  escreverCodigo(): void;
}

interface Bolsista {
  receberBolsa(): void;
}

interface Remuneravel {
  receberPorProjeto(): void;
}

class Gerente implements Trabalhavel, RegistraPonto, Assalariado, Gerenciavel {
  trabalhar(): void { console.log("Gerente trabalhando"); }
  registrarPonto(): void { console.log("Ponto registrado"); }
  receberSalario(): void { console.log("Salário recebido"); }
  gerenciarEquipe(): void { console.log("Gerenciando equipe"); }
}

class Desenvolvedor implements Trabalhavel, RegistraPonto, Assalariado, Programavel {
  trabalhar(): void { console.log("Desenvolvedor trabalhando"); }
  registrarPonto(): void { console.log("Ponto registrado"); }
  receberSalario(): void { console.log("Salário recebido"); }
  escreverCodigo(): void { console.log("Escrevendo código"); }
}

class Estagiario implements Trabalhavel, RegistraPonto, Bolsista, Programavel {
  trabalhar(): void { console.log("Estagiário trabalhando"); }
  registrarPonto(): void { console.log("Ponto registrado"); }
  receberBolsa(): void { console.log("Bolsa recebida"); }
  escreverCodigo(): void { console.log("Estagiário escrevendo código"); }
}

class Freelancer implements Trabalhavel, Programavel, Remuneravel {
  trabalhar(): void { console.log("Freelancer trabalhando"); }
  escreverCodigo(): void { console.log("Freelancer escrevendo código"); }
  receberPorProjeto(): void { console.log("Pagamento por projeto recebido"); }
}

class SistemaRH {
  private funcionarios: Trabalhavel[];

  constructor(funcionarios: Trabalhavel[]) {
    this.funcionarios = funcionarios;
  }

  iniciarJornada(): void {
    this.funcionarios.forEach(f => f.trabalhar());
  }
}

const sistema = new SistemaRH([
  new Gerente(),
  new Desenvolvedor(),
  new Estagiario(),
  new Freelancer()
]);

sistema.iniciarJornada();
