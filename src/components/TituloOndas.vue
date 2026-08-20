<template>
    <div class="titulo">
        <h1 class="contorno"> Tarefas: </h1>
        <h1 class="ondas"> Tarefas: </h1>
    </div>
</template>

<script>
</script>

<style>
.titulo{
    position: relative;
    margin-top: 5rem;
    margin-right: 20rem;
    text-align: center;
}

.titulo h1{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 6rem;
    margin: 0;
    white-space: nowrap;
}

.contorno{
    color: var(--color-contorno);
    -webkit-text-stroke: 2px var(--color-contorno);
}

.ondas{
    color: var(--color-ondas);
    z-index: 2;
    animation: onda 4s ease-in-out infinite;
}

@keyframes onda {
  0%, 100% {
    clip-path: polygon(
      0% 45%, 8% 47%, 16% 52%, 24% 58%, 32% 62%,
      40% 63%, 48% 61%, 56% 56%, 64% 50%, 72% 44%,
      80% 40%, 88% 39%, 96% 41%, 100% 43%,
      100% 100%, 0% 100%
    );
  }
  50% {
    clip-path: polygon(
      0% 40%, 8% 38%, 16% 40%, 24% 46%, 32% 52%,
      40% 56%, 48% 57%, 56% 55%, 64% 51%, 72% 48%,
      80% 47%, 88% 49%, 96% 52%, 100% 54%,
      100% 100%, 0% 100%
    );
  }
}
</style>