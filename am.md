AM:
<pre>
f_c = 100;          % carrier frequency (Hz)
f_m = 10;           % message frequency (Hz)
A_c = 1;            % carrier amplitude
A_m = 0.5;          % message amplitude
t = 0:0.001:1;      % time vector

% Generate message signal
m_t = A_m*sin(2*pi*f_m*t);

% Generate carrier signal
c_t = A_c*sin(2*pi*f_c*t);

% Modulate the carrier with the message signal
s_t = (1 + m_t).*c_t;

% Plot the signals
subplot(3,1,1);
plot(t, m_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Message signal');

subplot(3,1,2);
plot(t, c_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Carrier signal');

subplot(3,1,3);
plot(t, s_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('AM signal');
</pre>

FM:

<pre>
% Define parameters
f_c = 100;          % carrier frequency (Hz)
f_m = 10;           % message frequency (Hz)
A_c = 1;            % carrier amplitude
delta_f = 50;       % frequency deviation
t = 0:0.001:1;      % time vector

% Generate message signal
m_t = sin(2*pi*f_m*t);

% Generate carrier signal
c_t = A_c*sin(2*pi*f_c*t);

% Modulate the frequency of the carrier with the message signal
s_t = A_c*sin(2*pi*f_c*t + delta_f/f_m*cos(2*pi*f_m*t));

% Plot the signals
subplot(3,1,1);
plot(t, m_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Message signal');

subplot(3,1,2);
plot(t, c_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Carrier signal');

subplot(3,1,3);
plot(t, s_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('FM signal');

</pre>

PM:

<pre>
% Define parameters
f_c = 100;          % carrier frequency (Hz)
f_m = 10;           % message frequency (Hz)
A_c = 1;            % carrier amplitude
delta_phi = pi/2;   % phase deviation
t = 0:0.001:1;      % time vector

% Generate message signal
m_t = sin(2*pi*f_m*t);

% Generate carrier signal
c_t = A_c*sin(2*pi*f_c*t);

% Modulate the phase of the carrier with the message signal
s_t = A_c*sin(2*pi*f_c*t + delta_phi*m_t);

% Plot the signals
subplot(3,1,1);
plot(t, m_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Message signal');

subplot(3,1,2);
plot(t, c_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('Carrier signal');

subplot(3,1,3);
plot(t, s_t);
xlabel('Time (s)');
ylabel('Amplitude');
title('PM signal');

</pre>
