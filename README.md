# terraform53-1
remember-53-1

Terraform Uygulama (AWS EC2)
Adım adım bir EC2 örneği. AWS üzerinde bir EC2 instance (sanal sunucu) kuralım.

🔧 AWS hesabı
IAM kullanıcı erişim anahtarları (Access Key ID & Secret Access Key)
Terraform yüklü bir bilgisayar (Linux/Mac/Windows)

✅ Adım 1: Terraform Kurulumu
Linux/macOS:

bash:
sudo apt update
sudo apt install -y unzip curl
curl -fsSL https://releases.hashicorp.com/terraform/1.8.0/terraform_1.8.0_linux_amd64.zip -o terraform.zip
unzip terraform.zip
sudo mv terraform /usr/local/bin/
terraform -v
📁 Adım 2: Proje Dizini Oluştur
bash:
mkdir terraform-ec2
cd terraform-ec2
touch main.tf variables.tf outputs.tf
📝 Adım 3: main.tf içeriği
hcl:
provider "aws" {
  region     = "eu-central-1"
  access_key = var.aws_access_key
  secret_key = var.aws_secret_key
}
resource "aws_instance" "example" {
  ami           = "ami-0faab6bdbac9486fb" # Ubuntu 22.04 Frankfurt için örnek AMI
  instance_type = "t2.micro"
  tags = {
    Name = "TerraformExample"
  }
}
🔐 Adım 4: variables.tf içeriği
h:
variable "aws_access_key" {
  description = "AWS Access Key"
  type        = string
}
variable "aws_secret_key" {
  description = "AWS Secret Key"
  type        = string
}
📤 Adım 5: outputs.tf içeriği
hcl:
output "instance_public_ip" {
  value = aws_instance.example.public_ip
}
🧪 Adım 6: Terraform Komutları
bash:
terraform init        # Plugin’leri indirir
terraform plan        # Ne yapılacağını gösterir
terraform apply       # Uygulama yapar
📝 Uygulamada senden aws_access_key ve aws_secret_key isteyecektir. Terminalde girebilirsin veya .tfvars dosyasında tanımlayabilirsin.

🧹 Temizleme (Kaynakları silmek için):
bash:
terraform destroy

