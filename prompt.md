prompt: quiero que hagas un juego basico
ia: o1 OpenIa

import { useState, useEffect } from "react";
import { Button } from "@/components/ui/button";

export default function ClickSpeedGame() {
  const [count, setCount] = useState(0);
  const [timeLeft, setTimeLeft] = useState(10);
  const [isPlaying, setIsPlaying] = useState(false);

  useEffect(() => {
    if (isPlaying && timeLeft > 0) {
      const timer = setInterval(() => {
        setTimeLeft((prev) => prev - 1);
      }, 1000);
      return () => clearInterval(timer);
    } else if (timeLeft === 0) {
      setIsPlaying(false);
    }
  }, [isPlaying, timeLeft]);

  const startGame = () => {
    setCount(0);
    setTimeLeft(10);
    setIsPlaying(true);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen gap-4">
      <h1 className="text-2xl font-bold">Click Speed Game</h1>
      <p className="text-lg">Tiempo restante: {timeLeft} s</p>
      <p className="text-lg">Puntuación: {count}</p>
      <Button onClick={() => isPlaying && setCount(count + 1)} disabled={!isPlaying}>
        ¡Haz clic!
      </Button>
      {!isPlaying && <Button onClick={startGame}>Iniciar juego</Button>}
    </div>
  );
}

prompt: agrégale mas funcionalidades
ia: o1 OpenIa

import { useState, useEffect } from "react";
import { Button } from "@/components/ui/button";

export default function ClickSpeedGame() {
  const [count, setCount] = useState(0);
  const [timeLeft, setTimeLeft] = useState(10);
  const [isPlaying, setIsPlaying] = useState(false);
  const [bestScore, setBestScore] = useState(0);

  useEffect(() => {
    if (isPlaying && timeLeft > 0) {
      const timer = setInterval(() => {
        setTimeLeft((prev) => prev - 1);
      }, 1000);
      return () => clearInterval(timer);
    } else if (timeLeft === 0) {
      setIsPlaying(false);
      setBestScore((prev) => (count > prev ? count : prev));
    }
  }, [isPlaying, timeLeft, count]);

  const startGame = () => {
    setCount(0);
    setTimeLeft(10);
    setIsPlaying(true);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen gap-4">
      <h1 className="text-2xl font-bold">Click Speed Game</h1>
      <p className="text-lg">Tiempo restante: {timeLeft} s</p>
      <p className="text-lg">Puntuación: {count}</p>
      <p className="text-lg font-semibold">Mejor puntuación: {bestScore}</p>
      <Button onClick={() => isPlaying && setCount(count + 1)} disabled={!isPlaying}>
        ¡Haz clic!
      </Button>
      {!isPlaying && <Button onClick={startGame}>Iniciar juego</Button>}
    </div>
  );
}

prompt: He visto que cuando hago click el tiempo no baja, ¿lo puedes solucionar?
ia: o1 OpenIa

import { useState, useEffect } from "react";
import { Button } from "@/components/ui/button";

export default function ClickSpeedGame() {
  const [count, setCount] = useState(0);
  const [timeLeft, setTimeLeft] = useState(10);
  const [isPlaying, setIsPlaying] = useState(false);
  const [bestScore, setBestScore] = useState(0);

  useEffect(() => {
    if (isPlaying && timeLeft > 0) {
      const timer = setInterval(() => {
        setTimeLeft((prev) => Math.max(prev - 1, 0));
      }, 1000);
      return () => clearInterval(timer);
    } else if (timeLeft === 0) {
      setIsPlaying(false);
      setBestScore((prev) => (count > prev ? count : prev));
    }
  }, [isPlaying, timeLeft]);

  const startGame = () => {
    setCount(0);
    setTimeLeft(10);
    setIsPlaying(true);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen gap-4">
      <h1 className="text-2xl font-bold">Click Speed Game</h1>
      <p className="text-lg">Tiempo restante: {timeLeft} s</p>
      <p className="text-lg">Puntuación: {count}</p>
      <p className="text-lg font-semibold">Mejor puntuación: {bestScore}</p>
      <Button onClick={() => isPlaying && setCount((prev) => prev + 1)} disabled={!isPlaying}>
        ¡Haz clic!
      </Button>
      {!isPlaying && <Button onClick={startGame}>Iniciar juego</Button>}
    </div>
  );
}
