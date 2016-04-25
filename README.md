# 25.abril.2016
métodos para pronosticar datos (meanf, naive, rwf)

## 25 de abril de 2016 ##
## metodos para pronosticar datos
## meanf, naive, rwf

install.packages("fpp")
library (fpp)
install.packages("foreing")
library (foreing)
tasas <- read.csv("C:\\Users\\SALA-C9\\Desktop\\tasas inegi.csv")
participacion <- ts(tasas [,1], start = 2013, frequency = 4)
plot(participacion)
Acf(participacion)

## meanf (variable, h), h: periodo de tiempo que quiere pronosticar
## meanf pronostica la serie de tiempo a traves de la media
partpronosticado <- meanf(participacion, 4) ## 4 puntos en la grafica
View (partpronosticado)
plot(partpronosticado)

## metodo ingenuo agarra el ultimo valor de la serie de tiempo
partpronos2 <- naive(participacion, 3)
plot(partpronos2)
rwf(participacion, 3) ## alternativo, hace lo mismo que el naive

## ingenuo estacional
partpronos3 <- snaive(participacion, 4)
partpronos3
plot(partpronos3)

## metodo de la deriva
partpronos4 <- rwf(participacion, 4,drift = T ) ## es lo que activa que sea el metodo de la deriva
partpronos4
plot(partpronos4)

plot(partpronosticado, plot.conf =FALSE, main = "proyeccion de tasas de participacion, trimestral") ## plot.conf es para la parte grisesita o azul que se pone al final de la grafica
lines(partpronos2$mean, col = 10)
lines(partpronos3$mean, col = 30)
legend("topleft", lty = 5, col= c(1,10,30), legend = c("metodo media", "metodo ingenuo", "metodo ingenuo estacional"))

## otra forma, no quedo muy bien

plot(participacion, plot.conf =FALSE, main = "proyeccion de tasas de participacion, trimestral") 
lines(partpronosticado$mean, col = 100)
lines(partpronos2$mean, col = 200)
lines(partpronos3$mean, col = 300)
legend("topleft", lty = 5, col= c(1,100,200,300), legend = c("metodo media", "metodo ingenuo", "metodo ingenuo estacional"))
