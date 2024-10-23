# Giai đoạn 1: Build ứng dụng
FROM maven:3.8.5-openjdk-17 AS build

WORKDIR /app

# Sao chép file pom.xml và tải các dependencies cần thiết (sẽ giúp sử dụng cache hiệu quả)
COPY pom.xml ./
RUN mvn dependency:go-offline -B

# Sao chép toàn bộ mã nguồn và tiến hành build
COPY src ./src
RUN mvn clean package -DskipTests

# Giai đoạn 2: Chạy ứng dụng
FROM openjdk:17-jdk-alpine

# Tạo thư mục tạm thời
VOLUME /tmp

# Copy file JAR từ giai đoạn build
COPY --from=build /app/target/oauth2-0.0.1-SNAPSHOT.jar app.jar

# Chạy ứng dụng
ENTRYPOINT ["java","-jar","/app.jar"]
