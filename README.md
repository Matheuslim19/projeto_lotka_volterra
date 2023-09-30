# projeto_lotka_volterra

% Definir as equações Lotka-Volterra
% dx/dt = αx - βxy
% dy/dt = δxy - γy
% onde x é a população de presas e y é a população de predadores

% Definir os parâmetros
alpha = 0.1;
beta = 0.3;
gamma = 0.5;
delta = 0.1;
c=0.6;
a=0.9;

% Definir as condições iniciais
x0 = 10; % população inicial de presas
y0 = 10; % população inicial de predadores
initial_conditions = [x0, y0];

% Definir o intervalo de tempo de integração
tspan = [0, 100]; % tempo inicial e tempo final

% Definir o tamanho do passo de integração
h = 0.01; % tamanho do passo de integração

% Calcular o número de passos de integração
num_steps = ceil((tspan(2) - tspan(1)) / h);

% Inicializar os vetores para as soluções
t = zeros(num_steps + 1, 1);
x = zeros(num_steps + 1, 1);
y = zeros(num_steps + 1, 1);

% Atribuir as condições iniciais aos vetores de soluções
t(1) = tspan(1);
x(1) = x0;
y(1) = y0;

% Loop para a integração usando o método de Adams-Bashforth de segunda ordem
for i = 1:num_steps
    % Calcular as derivadas no tempo atual
    dx_dt =  a*x(i) - alpha * x(i) * y(i) - beta*x(i);
    dy_dt = -c*y(i) + gamma * x(i) * y(i) - delta * y(i);
    
    % Calcular as soluções usando o método de Adams-Bashforth de segunda ordem
    x(i + 1) = x(i) + h * dx_dt;
    y(i + 1) = y(i) + h * dy_dt;
    t(i + 1) = t(i) + h;
end

% Plotar as soluções
figure;
plot(t, x, 'b-', 'LineWidth', 1.5, 'DisplayName', 'Presas');
hold on;
plot(t, y, 'r-', 'LineWidth', 1.5, 'DisplayName', 'Predadores');
xlabel('Tempo');
ylabel('População');
title('Modelo Lotka-Volterra (Adams-Bashforth de 2ª ordem)');
legend('Presas', 'Predadores');
