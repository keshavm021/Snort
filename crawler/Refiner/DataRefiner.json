package crawler.Refiner;

import com.fasterxml.jackson.databind.ObjectMapper;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class DataRefiner
{

    static ObjectMapper mapper = new ObjectMapper();

    private static void saveJsonToFile(String path, String json) {

        try {
            FileWriter fileWriter = new FileWriter(path);

            fileWriter.write(json);
            fileWriter.flush();
            fileWriter.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        System.out.println("saved to file");

    }
    public static void main(String args[]) throws IOException {


        File file=new File("/home/lakshay/Desktop/mail-spam2.json");
        List<Map<String,Object>> dataList = mapper.readValue(file,List.class);
        List<Map<String,String>> outputData = new ArrayList<>();

        for(Map<String,Object> datamap : dataList) {
            Map<String,Object> source = (Map<String, Object>) datamap.get("_source");
            Map<String,Object> layers = (Map<String, Object>) source.get("layers");

            Map<String,String> refinedDataMap = new HashMap<>() ;


            try {
                Map<String,String> ethernet = (Map<String, String>) layers.get("eth");
                refinedDataMap.put("ethernetSource",ethernet.get("eth.src"));
                refinedDataMap.put("ethernetDestination",ethernet.get("eth.dst"));

                Map<String,String> ip = (Map<String, String>) layers.get("ip");
                refinedDataMap.put("ipSource",ip.get("ip.src"));
                refinedDataMap.put("ipDestination",ip.get("ip.dst"));

                Map<String,String> udp = (Map<String, String>) layers.get("udp");
                refinedDataMap.put("udpSourcePort",udp.get("udp.srcport"));
                refinedDataMap.put("udpDestinationPort",udp.get("udp.dstport"));
            }
            catch (NullPointerException e){

            }


            outputData.add(refinedDataMap);

        }

        System.out.println("Writing to file---");
        String json = mapper.writeValueAsString(outputData);
        saveJsonToFile("/home/lakshay/Desktop/refined-mail-spam2.json",json);
        System.out.println("Done");

    }
}
