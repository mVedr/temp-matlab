ASK:

%GENERATE CARRIER SIGNAL
Tb=1; fc=2; % same carrier frequency for both signals
t=0:(Tb/100):Tb;
c=sqrt(2/Tb)*sin(2*pi*fc*t);
%generate message signal
N=8;
m=rand(1,N);
t1=0;t2=Tb;
for i=1:N
    t=[t1:(Tb/100):t2];
    if m(i)>0.5
        m_s=ones(1,length(t));
    else
        m_s=zeros(1,length(t));
    end
    message(i,:)=m_s;
    %Multiplier
    ask_sig(i,:)=c.*(m_s*2-1);
    %plotting the message signal and the modulated signal
    subplot(3,2,2);axis([0 N -2 2]);plot(t,message(i,:),'r'); title('message signal');xlabel('t---->');ylabel('m(t)');grid on;hold on;
    subplot(3,2,5);plot(t,ask_sig(i,:));
    title('ASK signal');xlabel('t---->');ylabel('s(t)');grid on;hold on;
    t1=t1+(Tb+.01); t2=t2+(Tb+.01);
end
hold off
%Plotting binary data bits and carrier signal
subplot(3,2,1);stem(m);
title('binary data');xlabel('n---->');
ylabel('b(n)');grid on;
subplot(3,2,3);plot(t,c);
title('carrier signal');xlabel('t---->');ylabel('c(t)');grid on;
% ASK Demodulation
t1=0;t2=Tb;
for i=1:N
    t=[t1:(Tb/100):t2];
    %correlator
    x=sum(c.*ask_sig(i,:));
    %decision device
    if x>0
        demod(i)=1;
    else
        demod(i)=0;
    end
    t1=t1+(Tb+.01);
    t2=t2+(Tb+.01);
end
%Plotting the demodulated data bits
subplot(3,2,6);stem(demod);
title(' demodulated data');xlabel('n---->');ylabel('b(n)'); grid on;


FSK:

% GENERATE CARRIER SIGNAL
Tb=1; fc1=2;fc2=5;
t=0:(Tb/100):Tb;
c1=sqrt(2/Tb)*sin(2*pi*fc1*t);
c2=sqrt(2/Tb)*sin(2*pi*fc2*t);

% GENERATE MESSAGE SIGNAL
N=8;
m=rand(1,N);
t1=0;t2=Tb;
for i=1:N
    t=[t1:(Tb/100):t2];
    if m(i)>0.5
        m(i)=1;
        m_s=ones(1,length(t));
        invm_s=zeros(1,length(t));
    else
        m(i)=0;
        m_s=zeros(1,length(t));
        invm_s=ones(1,length(t));
    end
    message(i,:)=m_s;
    % MULTIPLIER
    fsk_sig1(i,:)=c1.*m_s;
    fsk_sig2(i,:)=c2.*invm_s;
    fsk=fsk_sig1+fsk_sig2;
    % PLOTTING THE MESSAGE SIGNAL AND THE MODULATED SIGNAL
    subplot(3,2,2);
    axis([0 N -2 2]);
    plot(t,message(i,:),'r');
    title('Message signal');
    xlabel('t---->');
    ylabel('m(t)');
    grid on;
    hold on;
    subplot(3,2,5);
    plot(t,fsk(i,:));
    title('FSK signal');
    xlabel('t---->');
    ylabel('s(t)');
    grid on;
    hold on;
    t1=t1+(Tb+.01);
    t2=t2+(Tb+.01);
end
hold off

% PLOTTING BINARY DATA BITS AND CARRIER SIGNAL
subplot(3,2,1);
stem(m);
title('Binary data');
xlabel('n---->');
ylabel('b(n)');
grid on;
subplot(3,2,3);
plot(t,c1);
title('Carrier signal-1');
xlabel('t---->');
ylabel('c1(t)');
grid on;
subplot(3,2,4);
plot(t,c2);
title('Carrier signal-2');
xlabel('t---->');
ylabel('c2(t)');
grid on;

% FSK DEMODULATION
t1=0;t2=Tb;
for i=1:N
    t=[t1:(Tb/100):t2];
    % CORRELATOR
    x1=sum(c1.*fsk_sig1(i,:));
    x2=sum(c2.*fsk_sig2(i,:));
    x=x1-x2;
    % DECISION DEVICE
    if x>0
        demod(i)=1;
    else
        demod(i)=0;
    end
    t1=t1+(Tb+.01);
    t2=t2+(Tb+.01);
end

% PLOTTING THE DEMODULATED DATA BITS
subplot(3,2,6);
stem(demod);
title('Demodulated data');
xlabel('n---->');
ylabel('b(n)');
grid on;


PSK:
%Phase Shift Key

%GENERATE CARRIER SIGNAL
Tb=1;
t=0:Tb/100:Tb;
fc=2;
c=sqrt(2/Tb)*sin(2*pi*fc*t);
%generate message signal
N=8;
m=rand(1,N);
t1=0;t2=Tb;
for i=1:N
    t=[t1:.01:t2];
    if m(i)>0.5
        m(i)=1;
        m_s=ones(1,length(t));
    else
        m(i)=0;
        m_s=-1*ones(1,length(t));
    end
    message(i,:)=m_s;
    %product of carrier and message signal
    bpsk_sig(i,:)=c.*m_s;
    %Plot the message and BPSK modulated signal
    subplot(5,1,2);axis([0 N -2 2]);plot(t,message(i,:),'r');
    title('message signal(POLAR form)');xlabel('t--->');ylabel('m(t)');
    grid on; hold on;
    subplot(5,1,4);plot(t,bpsk_sig(i,:));
    title('BPSK signal');xlabel('t--->');ylabel('s(t)');
    grid on; hold on;
    t1=t1+1.01; t2=t2+1.01;
end
hold off
%plot the input binary data and carrier signal
subplot(5,1,1);stem(m);
title('binary data bits');xlabel('n--->');ylabel('b(n)');
grid on;
subplot(5,1,3);plot(t,c);
title('carrier signal');xlabel('t--->');ylabel('c(t)');
grid on;
% PSK Demodulation
t1=0;t2=Tb;
for i=1:N
    t=[t1:.01:t2];
    %correlator
    x=sum(c.*bpsk_sig(i,:));
    %decision device
    if x>0
        demod(i)=1;
    else
        demod(i)=0;
    end
    t1=t1+1.01;
    t2=t2+1.01;
end
%plot the demodulated data bits
subplot(5,1,5);stem(demod);
title('demodulated data');xlabel('n--->');ylabel('b(n)'); 
