# Abdullah-Samet-Bayraktar
JPEG ALGORİTMASI KOD BLOĞUMUZ
package jpegcompressor;

import java.awt.image.RenderedImage;
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.IOException;
import javax.imageio.IIOImage;
import javax.imageio.ImageIO;
import javax.imageio.ImageWriter;
import javax.imageio.ImageWriteParam;
import javax.imageio.stream.ImageOutputStream;
import javax.imageio.stream.MemoryCacheImageOutputStream;

public class JPEGCompressor {

    public static void main(String[] args) {
        File orjinalResim = new File("C:\\Users\\SERDAR\\Desktop\\samet.jpeg");
        File compressedResim = new File("C:\\Users\\SERDAR\\Desktop\\compressedResim5.jpeg");
        try {
            CompressJPEGResmi(orjinalResim, compressedResim, 0.587f);
            System.out.println("SIKIŞTIRMA İŞLEMİ BAŞARILI BİR ŞEKİLDE TAMAMLANDI");
        } catch (IOException e) {
        }
    }

    public static void CompressJPEGResmi(File orjinalResim, File compressedResim, float Kalite) throws IOException {
        RenderedImage resim = ImageIO.read(orjinalResim);
        ImageWriter jpegyazici = ImageIO.getImageWritersByFormatName("jpg").next();
        ImageWriteParam jpegresimyazici = jpegyazici.getDefaultWriteParam();
        jpegresimyazici.setCompressionMode(ImageWriteParam.MODE_EXPLICIT);
        jpegresimyazici.setCompressionQuality(Kalite);

        try (ImageOutputStream cikti = ImageIO.createImageOutputStream(compressedResim)) {
            jpegyazici.setOutput(cikti);
            IIOImage resimciktisi = new IIOImage(resim, null, null);
            jpegyazici.write(null, resimciktisi, jpegresimyazici);
        }
        jpegyazici.dispose();
    }
}
