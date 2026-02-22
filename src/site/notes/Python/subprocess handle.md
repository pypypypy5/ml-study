---
{"dg-publish":true,"permalink":"/python/subprocess-handle/"}
---



```jsx
cmd = [
            "accelerate", "launch",
            "--num_cpu_threads_per_process=2",
            str(self.train_script),
            "--config_file", str(config_path)
        ]

        logger.info(f"[LoRATrainer] Command: {' '.join(cmd)}")

        # Run training process
        process = await asyncio.create_subprocess_exec(
            *cmd,
            stdout=asyncio.subprocess.PIPE,
            stderr=asyncio.subprocess.STDOUT,
            cwd=str(Path("/kohya"))
        )

        # Stream output
        async for line in process.stdout:
```

*cmd는 원소를 펼쳐서 accelerate, launch, …가 바로 들어가게 하는 방법.

asyncio로 서브 프로세스를 만들고, 그 서브 프로세스 안에서 cmd를 펼친 명령어들을 실행시켜 내부에서 여러 epoch을 거치며 학습이 이루어지도록 하는 것이다. 이때 process 객체 안에 PIPE를 사용하면 .stdout으로 프로세스의 stdout을 기다리지 않고 나오는대로 받고, 사용하는 방식.