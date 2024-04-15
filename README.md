# controledeacesso
exercicio-controle-de-acesso

const readlineSync = require('readline-sync');

const nome = readlineSync.question("Digite seu nome: ");
const nivelAcesso = readlineSync.question("Digite seu nível de acesso (visitante, funcionário, gerente ou administrador): ");
const horarioAcesso = readlineSync.question("Digite o horário de acesso (hora e minuto): ");

const hora = parseInt(horarioAcesso.split(":")[0]);
const minuto = parseInt(horarioAcesso.split(":")[1]);
const horarioFuncionamento = {
  inicio: 8,
  fim: 22,
};
const horarioVisitas = {
  inicio: 9,
  fim: 18,
};

if (
  (horarioFuncionamento.inicio <= hora && hora <= horarioFuncionamento.fim) ||
  (nivelAcesso === "visitante" &&
    horarioVisitas.inicio <= hora &&
    hora <= horarioVisitas.fim &&
    horarioFuncionamento.inicio <= hora &&
    hora <= horarioFuncionamento.fim)
) {
  if (nivelAcesso === "visitante" && hora < horarioVisitas.inicio) {
    console.log("Desculpe, o horário de visitas ainda não começou.");
  } else if (nivelAcesso === "visitante" && hora > horarioVisitas.fim) {
    console.log("Desculpe, o horário de visitas já terminou.");
  } else if (nivelAcesso === "funcionário" && hora < horarioFuncionamento.inicio) {
    console.log("Desculpe, o prédio ainda não está aberto.");
  } else if (nivelAcesso === "funcionário" && hora > horarioFuncionamento.fim) {
    console.log("Desculpe, o prédio já fechou.");
  } else {
    console.log("Bem-vindo(a) ao prédio!");
  }
} else {
  console.log("Desculpe, o prédio está fechado ou o horário de visitas não é permitido.");
}
