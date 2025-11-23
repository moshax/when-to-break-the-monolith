# Background Image Processing Worker

## 🧠 Context
Image manipulation tasks (resize, watermark, thumbnails) are CPU-heavy and should not run on the main web process. Offloading them improves frontend responsiveness.

## 🎯 Goal
Move resource-intensive image processing to an async worker service:
- Decouples processing from user-facing requests
- Increases system throughput
- Improves user experience by returning responses faster

## 🛠 Architecture Sketch
- User uploads image via MainApp
- MainApp emits `ImageUploaded` event
- ImageWorker consumes event, processes image, stores result (e.g. S3)
- Optional: Notify MainApp or user when done

## ✅ Implementation Tips
- Use local Docker volume for image handling
- Consider RabbitMQ or SQS for message queue
- Use libraries like Sharp (Node.js), Glide (Java), or ImageSharp (.NET)
