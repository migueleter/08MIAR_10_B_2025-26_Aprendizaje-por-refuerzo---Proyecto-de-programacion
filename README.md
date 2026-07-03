# 🎮 Proyecto de Programación — Aprendizaje por Refuerzo (08MIAR)

Agente **Deep Q-Network (DQN)** 🤖 entrenado para jugar a **Space Invaders** 👾 (Atari), desarrollado para la asignatura *Aprendizaje por Refuerzo* del Máster en Inteligencia Artificial (VIU).

**👥 Grupo 3**
- Miguel Arribas Ramos
- Rafael Collado Molina
- Alex García Prats
- Marc González Pastor

## 🎯 Objetivo

Entrenar un agente que supere una **recompensa media > 20** en 100 episodios de test, aplicando las técnicas de la sesión de DQN (experience replay, red objetivo, exploración ε-greedy con annealing, reward clipping y Huber loss).

## 🧪 Propuestas evaluadas

Se comparan tres variantes, activadas mediante los flags nativos de `DQNAgent` (keras-rl2):

| Propuesta | Técnica | Configuración |
|-----------|---------|---------------|
| P1 | DQN base (*vanilla*) | `enable_double_dqn=False` |
| P2 | Double DQN | `enable_double_dqn=True` |
| P3 | Dueling + Double DQN | `enable_dueling_network=True`, `dueling_type='avg'` |

- **Comparativa** de las tres propuestas: entorno `SpaceInvaders-v0` (con *sticky actions* y frameskip estocástico).
- **Modelo final**: Dueling + Double DQN sobre `SpaceInvadersDeterministic-v4` (frameskip fijo, sin *sticky actions*), donde el aprendizaje es más estable y se supera el umbral.

## 🏆 Resultado

Modelo final (Dueling + Double DQN, `SpaceInvadersDeterministic-v4`, 100 episodios de test):

| Métrica | Valor |
|---------|-------|
| Recompensa media | **27.36** |
| Desviación típica | 7.21 |
| Mín / Máx | 11.0 / 58.0 |
| ¿Supera el umbral 20? | **Sí** |

## 📂 Contenido del repositorio

- `Proyecto_08MIAR_Grupo3.ipynb` — notebook con la solución completa: implementación de la red (arquitectura de Mnih et al., 2015), montaje del agente DQN, entrenamiento, evaluación del modelo final, justificación de hiperparámetros y discusión de resultados.
- `08MIAR_Grupo3_video_entrenamiento.mp4` — vídeo del **entrenamiento** (10x) del agente en ejecución (variante Dueling + Double DQN).
- `08MIAR_Grupo3_gameplay_modelo_final.mp4` — vídeo del **modelo final entrenado jugando** a Space Invaders.

> **Pesos entrenados (`.h5f`)**: no se versionan en GitHub por su tamaño; se entregan aparte en el ZIP de la actividad.

## ⚙️ Entorno de ejecución

Stack "clásico" requerido por el enunciado (Python 3.8):

```
gym==0.17.3
keras-rl2==1.0.5
tensorflow==2.5.3
atari-py (fork de Kojoley)
pyglet==1.5.0
h5py==3.1.0
Pillow==9.5.0
```

El notebook está preparado para **Google Colab** (instala las dependencias e importa desde Google Drive) y para ejecución **local**.

## ▶️ Cómo ejecutar

1. Abrir `Proyecto_08MIAR_Grupo3.ipynb` (Colab o Jupyter con un kernel de Python 3.8 y las dependencias anteriores).
2. Ejecutar las celdas en orden: configuración → red → agente DQN → evaluación del modelo final.
3. El entrenamiento completo es largo (~7 h en CPU para el modelo final); por defecto está desactivado (`RUN_TRAINING = False`) y las celdas de evaluación cargan los pesos ya entrenados. Para reentrenar, poner `RUN_TRAINING = True`.

