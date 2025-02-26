# similar-fc-24
similar fc 24
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FC24 Like Game</title>
    <style>
        body { background: green; text-align: center; }
        canvas { border: 2px solid white; }
    </style>
</head>
<body>
    <h1>FC24 Like Game</h1>
    <script src="game.js"></script>
</body>
</html>
const canvas = document.createElement("canvas");
const ctx = canvas.getContext("2d");
document.body.appendChild(canvas);
canvas.width = 800;
canvas.height = 400;

const player = {
  x: 100,
  y: 200,
  width: 20,
  height: 20,
  speed: 4,
  color: "blue",
};

const ball = {
  x: 400,
  y: 200,
  radius: 8,
  dx: 2,
  dy: 2,
  color: "white",
};

const keys = {};

document.addEventListener("keydown", (e) => (keys[e.key] = true));
document.addEventListener("keyup", (e) => (keys[e.key] = false));

function movePlayer() {
  if (keys["ArrowUp"] && player.y > 0) player.y -= player.speed;
  if (keys["ArrowDown"] && player.y < canvas.height - player.height)
    player.y += player.speed;
  if (keys["ArrowLeft"] && player.x > 0) player.x -= player.speed;
  if (keys["ArrowRight"] && player.x < canvas.width - player.width)
    player.x += player.speed;
}

function moveBall() {
  ball.x += ball.dx;
  ball.y += ball.dy;
  if (ball.y + ball.radius > canvas.height || ball.y - ball.radius < 0) {
    ball.dy *= -1;
  }
}

function drawPlayer() {
  ctx.fillStyle = player.color;
  ctx.fillRect(player.x, player.y, player.width, player.height);
}

function drawBall() {
  ctx.fillStyle = ball.color;
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
  ctx.fill();
}

function update() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  movePlayer();
  moveBall();
  drawPlayer();
  drawBall();
  requestAnimationFrame(update);
}

update();
