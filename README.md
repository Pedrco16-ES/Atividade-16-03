# Atividade-16-03
Solid
---part 1
ISP – Interface Segregation Principle
Trecho violado: A interface Funcionario possui 5 métodos obrigatórios para todos.
Por que é violação: Classes são forçadas a implementar métodos que não fazem sentido para elas. Gerente não escreve código, Desenvolvedor não gerencia equipe, Estagiário não recebe salário.
Impacto: Qualquer novo tipo de funcionário precisa implementar todos os métodos, mesmo os irrelevantes, gerando acoplamento desnecessário.

LSP – Liskov Substitution Principle
Trecho violado: Métodos que lançam throw new Error(...) nas subclasses.
Gerente.escreverCodigo()     → throw new Error("Gerente não escreve código")
Desenvolvedor.gerenciarEquipe() → throw new Error("Dev não gerencia equipe")
Estagiario.receberSalario()  → throw new Error("Estagiário recebe bolsa...")
Estagiario.gerenciarEquipe() → throw new Error("Estagiário não gerencia")
Por que é violação: Se você substituir Funcionario por qualquer dessas classes, o programa pode quebrar em tempo de execução — violando a premissa do LSP.
Impacto: Código cliente não pode confiar que um Funcionario genérico funcionará corretamente.

DIP – Dependency Inversion Principle
Trecho violado: Não existe nenhuma classe de alto nível (ex: SistemaRH) — mas se existisse usando new Gerente(), new Desenvolvedor() diretamente, violaria o DIP.

Por que é violação: Módulos de alto nível dependem de implementações concretas, não de abstrações.
Impacto: Dificulta troca de implementações e testes unitários.

---part 2

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
